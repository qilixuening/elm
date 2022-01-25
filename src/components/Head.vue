<template>
  <header id="head-container">
    <slot name="logo" />
    <slot name="search" />
    <section
      class="head_goback"
      v-if="goBack"
      @click="$router.back()"
    >
      <svg
       width="100%"
       height="100%"
       xmlns="http://www.w3.org/2000/svg"
       version="1.1"
      >
        <polyline
          points="12,18 4,9 12,0"
          style="fill:none; stroke:rgb(255,255,255); stroke-width:2"
        />
      </svg>
    </section>

    <router-link
      class="head_login"
      v-if="signinUp"
      :to="userInfo ? '/profile' : '/login'"
    >
      <svg
        class="user_avatar"
        v-if="userInfo"
      >
        <use
          xmlns:xlink="http://www.w3.org/1999/xlink"
          xlink:href="#user"
        />
      </svg>
      <span
        class="login_span"
        v-else
      >
        登录|注册
      </span>
    </router-link>
    <section
      class="title_head ellipsis"
      v-if="headTitle"
    >
      <span class="title_text">
        {{ headTitle }}
      </span>
    </section>
    <slot name="edit" />
    <slot name="msite-title" />
    <slot name="changecity" />
    <slot name="changeLogin" />
  </header>
</template>
