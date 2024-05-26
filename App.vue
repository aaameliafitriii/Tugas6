<template>
    <div class="container">
      <h1>Manajemen Artikel</h1>
      <form @submit.prevent="save" class="form">
        <input type="text" v-model="form.title" placeholder="Judul" required/><br />
        <textarea v-model="form.content" placeholder="Konten" required></textarea><br />
        <button type="submit">Simpan</button>
        <button type="button" @click="resetForm">Reset</button>
      </form>
      <div class="articles">
        <h2>Daftar Artikel</h2>
        <ul>
          <li v-for="article in articles" :key="article.id" class="article-item">
            <div class="article-content">
              <strong>{{ article.title }}</strong><br />
              <p>{{ article.content }}</p>
            </div>
            <div class="article-actions">
              <button @click="edit(article)">Edit</button>
              <button @click="remove(article.id)">Hapus</button>
            </div>
          </li>
        </ul>
        <button @click="load" class="load-button">Muat Data</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        articles: [],
        form: {
          id: null,
          title: "",
          content: ""
        }
      };
    },
    methods: {
      load() {
        // Simulasi pemuatan data dari JSON
        this.articles = [
          { id: 1, title: "Judul 1", content: "Ini Konten 1" },
          { id: 2, title: "Judul 2", content: "Ini Konten 2" },
          { id: 3, title: "Judul 3", content: "Ini Konten 3" }
        ];
      },
      save() {
        if (this.form.id) {
          const index = this.articles.findIndex(a => a.id === this.form.id);
          this.articles[index] = { ...this.form };
        } else {
          const newId = this.articles.length ? this.articles[this.articles.length - 1].id + 1 : 1;
          this.articles.push({ ...this.form, id: newId });
        }
        this.resetForm();
      },
      edit(article) {
        this.form = { ...article };
      },
      remove(id) {
        this.articles = this.articles.filter(article => article.id !== id);
      },
      resetForm() {
        this.form.id = null;
        this.form.title = "";
        this.form.content = "";
      }
    }
  };
  </script>
  
  <style>
  .container {
    max-width: 600px;
    margin: auto;
    padding: 20px;
    font-family: Arial, sans-serif;
  }
  
  h1, h2 {
    text-align: center;
  }
  
  .form {
    margin-bottom: 20px;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 4px;
    background-color: #f9f9f9;
  }
  
  .form input, .form textarea {
    width: calc(100% - 20px);
    padding: 10px;
    margin: 5px 0;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  
  .form button {
    padding: 10px 20px;
    margin: 5px;
    border: none;
    border-radius: 4px;
    background-color: #28a745;
    color: white;
    cursor: pointer;
  }
  
  .form button[type="button"] {
    background-color: #ffc107;
  }
  
  .form button:hover {
    opacity: 0.9;
  }
  
  .articles {
    margin-top: 20px;
  }
  
  .article-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    margin: 10px 0;
    border: 1px solid #ddd;
    border-radius: 4px;
    background-color: #fff;
  }
  
  .article-content {
    flex: 1;
  }
  
  .article-actions {
    display: flex;
    gap: 10px;
  }
  
  .article-actions button {
    padding: 5px 10px;
    border: none;
    border-radius: 4px;
    background-color: #007bff;
    color: white;
    cursor: pointer;
  }
  
  .article-actions button:nth-child(2) {
    background-color: #dc3545;
  }
  
  .article-actions button:hover {
    opacity: 0.9;
  }
  
  .load-button {
    display: block;
    width: 100%;
    padding: 10px 0;
    border: none;
    border-radius: 4px;
    background-color: #007bff;
    color: white;
    cursor: pointer;
    margin-top: 10px;
  }
  
  .load-button:hover {
    opacity: 0.9;
  }
  </style>
  