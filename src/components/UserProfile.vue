<template>
  <div class="profile">
    <img v-lazy="profileImg" class="profile__img"/>

    <a class="thropy"  title="See Git Award"
      :href="'http://git-awards.com/users/search?login=' + userData.login" target="_blank">
      <i class="fa fa-trophy" aria-hidden="true"></i>
    </a>

    <div class="is-bookmarked" 
      :class="{'is-bookmarked--yes' : isBookmarked}" title="Bookmark User"
      @click="bookmarkUser">
      <svg version="1.1" width="30" height="48" viewBox="0 0 10 16" class="octicon octicon-bookmark" aria-hidden="true"><path fill-rule="evenodd" d="M9 0H1C.27 0 0 .27 0 1v15l5-3.09L10 16V1c0-.73-.27-1-1-1zm-.78 4.25L6.36 5.61l.72 2.16c.06.22-.02.28-.2.17L5 6.6 3.12 7.94c-.19.11-.25.05-.2-.17l.72-2.16-1.86-1.36c-.17-.16-.14-.23.09-.23l2.3-.03.7-2.16h.25l.7 2.16 2.3.03c.23 0 .27.08.09.23h.01z"/></svg>
    </div>
    
    <div class="profile__identity">
      <div class="profile__name">{{ userData.name }}</div>
      <small class="profile__login">{{ userData.login }}</small>      
    </div>

    <div class="profile__bio">
      {{ userData.bio }}     
    </div>
  </div>
</template>

<script>

export default {
  // http://git-awards.com/users/search?login=mazipan
  name: 'userprofile',
  props: ['userData', 'isBookmarked'],
  computed: {
    profileImg: function () {
      let self = this
      let img = '/explore-github/images/brand.png'
      if (self.userData && self.userData.avatar_url) {
        img = self.userData.avatar_url
      }
      return img
    }
  },
  methods: {
    bookmarkUser: function () {
      if (!this.isBookmarked) {
        this.$store.commit('setBookmarkUser', this.userData.login)
      } else alert('User has been bookmarked')
    }
  }
}
</script>

<style lang="scss" scoped>
  .profile{
    text-align: center;
    color: #282828;

    &__img{
      height: 100px;
      border-radius: 50%;
      border: 5px solid #0096d9;
    }

    &__identity, &__bio {
      margin-bottom: 10px;
    }

    &__name{
      font-size: 24px;
      margin: 10px 0 0px;
    }

    &__login {
      color: #a49c9c;
      font-size: 16px;
    }

  }
  .thropy{    
    position: absolute;
    top: 70px;
    left: 10px;
    cursor: pointer;
    color: #0096d9;
    font-size: 50px;
  }
  .is-bookmarked{
    position: absolute;
    top: 70px;
    right: 10px;
    cursor: pointer;

    &--yes{
      color: #0096d9;
    }
  }

</style>
