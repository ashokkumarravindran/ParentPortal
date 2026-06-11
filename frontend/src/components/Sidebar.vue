<template>
  <v-navigation-drawer
    permanent
    width="88"
    class="sidebar"
  >
    <div class="sidebar-top">
      <div class="state-mark">NY</div>
      <div class="state-label">
        <span>NEW</span>
        <span>YORK</span>
        <span>STATE</span>
      </div>
    </div>

    <v-divider class="sidebar-divider" />

    <div class="sidebar-nav">
      <v-btn icon="mdi-home-outline" class="nav-btn active" />
      <v-btn icon="mdi-magnify" class="nav-btn" />
      <v-btn icon="mdi-file-document-outline" class="nav-btn" />
      <v-btn icon="mdi-message-text-outline" class="nav-btn" />
      <v-btn icon="mdi-calendar-month-outline" class="nav-btn" />
    </div>

    <div class="sidebar-bottom">
      <v-btn icon="mdi-cog-outline" class="nav-btn" />
      <v-btn icon="mdi-help-circle-outline" class="nav-btn" />
      <v-btn icon="mdi-logout" class="nav-btn logout" />
    </div>
  </v-navigation-drawer>
</template>