<template>
  <div class="page-wrap">

    <el-form :model="controls"
             :rules="rules"
             ref="form"
             @submit.native.prevent="onSubmit">
      <h1 class="mb">Создание поста</h1>

      <el-form-item label="Введите название поста" prop="title">
        <el-input v-model="controls.title" />
      </el-form-item>

      <el-form-item label="Текст в формате .md или .html" prop="text">
        <el-input
          type="textarea"
          v-model="controls.text"
          resize="none"
          :rows="10"/>

      </el-form-item>

      <el-dialog title="Предпросмотр" :visible.sync="previewDialog">
        <div :key="controls.text">
          <vue-markdown>{{controls.text}}</vue-markdown>
        </div>
      </el-dialog>

      <el-upload
        class="mb"
        drag
        ref="upload"
        action="https://jsonplaceholder.typicode.com/posts/"
        :on-change="handleImageChange"
        :auto-upload="false"
      >
        <i class="el-icon-upload"></i>
        <div class="el-upload__text">Перетащите картинку <em>или нажмите</em></div>
        <div class="el-upload__tip" slot="tip">Только расширения: jpg/png</div>
      </el-upload>

      <el-button class="mb" type="success" plain @click="previewDialog = true">
        Предпросмотр
      </el-button>

      <el-form-item>
        <el-button type="primary"
                   native-type="submit"
                   :loading="loading"
                   round
        >
          Создать пост
        </el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
    export default {
      layout: 'admin',
      middleware: ['admin-auth'],
      data() {
        return {
          image: null,
          previewDialog: false,
          loading: false,
          controls: {
            title: '',
            text: ''
          },
          rules: {
            title: [{
              required: true,
              message: 'Текст поста не должен быть пустым',
              trigger: 'blur'
            }],
            text: [{
              required: true,
              message: 'Текст не должен быть пустым',
              trigger: 'blur'
            }]
          }
        }
      },
      methods: {
        handleImageChange(file, fileList) {
          this.image = file.raw
        },
        onSubmit() {
          this.$refs.form.validate(async valid => {
            if (valid && this.image) {
              this.loading = true

              const formData = {
                title: this.controls.title,
                text: this.controls.text,
                image: this.image
              }

              try {

                await this.$store.dispatch('post/create', formData)
                this.controls.title = ''
                this.controls.text = ''
                this.$refs.upload.clearFiles()
                this.image = null
                this.$message.success('Пост создан')

              } catch (e) {

              } finally {
                this.loading = false
              }
            } else {
              this.$message.warning('Форма не валидна')
            }
          })
        }
      }
    }
</script>

<style lang="scss" scoped>
  .page-wrap {
    max-width: 800px;
  }
  .mr {
    margin-right: 2rem;
  }
</style>
