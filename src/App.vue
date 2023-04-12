<script setup>
import {  ref } from 'vue'
import { messagesList } from '@/db'
import { navItems } from '@/components/constants/nav-items'

const messages = ref(messagesList)

const isActive = (numMessages) => {
  return numMessages > 0;
}
const currentItemMenu =ref('Chats')
</script>

<template>
  <header class="header">
    <div class="header__main">
      <h1 class="header__title">WhatsApp</h1>
      <div class="header__options">
        <i class="material-icons header__icon">search</i>
        <i class="material-icons header__icon">message</i>
        <i class="material-icons header__icon">more_vert</i>
      </div>
  </div>
  <nav class="nav">
    <ul class="nav__list">
      <li v-for="(item, index) in navItems" class="nav__item" :class="{ 'nav__item--active': currentItemMenu === item}" :key="index"><h3 class="nav__text">{{ item }}</h3></li>
  </ul>
  </nav>
  </header>
  <main class="chats">
    <ul class="chats__list">
      <li v-for="message in messages" :key="message.id" class="chat__item">
        <img :src="message.avatar" :alt="`${message.name} profile image`" class="chat__photo"/>
        <div class="chat__container">
          <div class="chat__content">
            <h2 class="chat__name">{{ message.name }}</h2>
            <p class="chat__text">
              <i class="material-icons chat__icon" :class="{'chat__icon--checked' : message.readConfirmation}"><span class="material-symbols-outlined">
              done_all
              </span></i>
              {{ message.short }}
            </p>
          </div>
          <div class="chat__extra">
            <p class="chat__time" :class="{ 'chat__time--active' : isActive(message.numMessages )}">{{ message.date.toLocaleTimeString('es-ES') }}</p>
            <p v-if="message.numMessages > 0" class="chat__amount">{{ message.numMessages }}</p>
          </div>
      </div>
      </li>
    </ul>
  </main>
</template>

<style lang="scss" scoped>
@import '@/assets/scss/header';
@import '@/assets/scss/chats';
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;500;600&display=swap');
</style>
