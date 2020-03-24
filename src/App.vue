<template>
  <div id="app">
    <div class="" style="margin-bottom: 20px">
      <!-- A grey horizontal navbar that becomes vertical on small screens -->
      <nav class="navbar navbar-expand-sm bg-dark navbar-dark">

        <!-- Links -->
        <ul class="navbar-nav">
          <li class="nav-item">
            <a class="nav-link" href="#">Latihan CRUD Vue JS</a>
          </li>
          <!-- <li class="nav-item">
            <a class="nav-link" href="#">Link 2</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">Link 3</a>
          </li> -->
        </ul>

      </nav>
    </div>
    <router-view></router-view>
  </div>
</template>

<script>
export default {

}
</script>

<style>

</style>