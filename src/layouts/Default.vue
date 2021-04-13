<template>
  <div class="layout">
    <header class="header">
      <strong>
        <g-link to="/" class='home-icon'></g-link>
      </strong>
      <nav class="nav">
        <g-link class="nav__link" to="/tag">类型</g-link>
        <g-link class="nav__link" to="/about/">推荐</g-link>
      </nav>
    </header>
    <slot/>
  </div>
</template>

<style>
body {
  font-family: -apple-system,system-ui,BlinkMacSystemFont,"Segoe UI",Roboto,"Helvetica Neue",Arial,sans-serif;
  margin:0;
  padding:0;
  line-height: 1.5;
}

.home-icon {
  display: block;
  width: 120px;
  height: 60px;
  background-size: cover;
  background-image: url('../../static/img/logo.jpg');
}

.header {
  position: fixed;
  top: 0;
  left: 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  box-sizing: border-box;
  background-color: rgba(0, 0, 0, 0.753);
  width: 100%;
  padding: 0 300px;
  height: 80px;
}

.nav__link {
  margin-left: 20px;
  font-size: 20px;
  color: #fff;
  font-weight: bold;
  text-decoration: none;
}
</style>
