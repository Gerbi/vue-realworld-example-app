<template>
  <div class="profile-page">
    <div class="user-info">
      <div class="container">
        <div class="row">
          <div class="col-xs-12 col-md-10 offset-md-1">
            <img :src="profile.image" class="user-img"/>
            <h4>{{ profile.username }}</h4>
            <p>
              {{ profile.bio }}
            </p>
            <button class="btn btn-sm btn-secondary action-btn" v-if="profile.following" @click.prevent="unfollow()">
              <i class="ion-checkmark-round"></i>
              Following {{ profile.username }}
            </button>
            <button class="btn btn-sm btn-outline-secondary action-btn" v-if="!profile.following" @click.prevent="follow()">
              <i class="ion-plus-round"></i>
              Follow {{ profile.username }}
            </button>
          </div>

        </div>
      </div>
    </div>

    <div class="container">
      <div class="row">
        <div class="col-xs-12 col-md-10 offset-md-1">
          <div class="articles-toggle">
            <ul class="nav nav-pills outline-active">
              <li class="nav-item">
                <router-link class="nav-link" active-class="active" :to="{ name: 'profile-articles' }">
                  My Articles
                </router-link>
              </li>
              <li class="nav-item">
                <router-link class="nav-link" active-class="active" :to="{ name: 'profile-favorited' }">
                  Favorited Articles
                </router-link>
              </li>
            </ul>
          </div>
          <router-view></router-view>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
  import { FETCH_PROFILE, FETCH_PROFILE_FOLLOW, FETCH_PROFILE_UNFOLLOW } from '@/store/actions.type'
  import { GET_PROFILE } from '@/store/getters.type'

  export default {
    name: 'RwvProfile',
    mounted () {
      this.$store.dispatch(FETCH_PROFILE, this.$route.params)
    },
    computed: {
      profile () {
        return this.$store.getters[GET_PROFILE]
      }
    },
    methods: {
      follow () {
        this.$store.dispatch(FETCH_PROFILE_FOLLOW, this.$route.params)
      },
      unfollow () {
        this.$store.dispatch(FETCH_PROFILE_UNFOLLOW, this.$route.params)
      }
    },
    watch: {
      $route (to) {
        this.$store.dispatch(FETCH_PROFILE, to.params)
      }
    }
  }
</script>