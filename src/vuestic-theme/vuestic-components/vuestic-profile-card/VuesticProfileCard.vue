<template>
  <div class="vuestic-profile-card d-flex flex-column align-items-center">
    <div class="photo">
      <img :src="photoSource" />
    </div>
    <h5 class="name text-md-center">{{name}}</h5>
    <span class="location"><span class="icon glyphicon glyphicon-education"></span> {{location}}</span>
    <div class="social">
     <a class="icon brandico brandico-linkedin"
         v-if="social.instagram" :href="'http://' + social.instagram" target="_blank"></a>
      <a class=" btn-lg glyphicon glyphicon-envelope"
         v-if="social.linkedin" :href="'http://' + social.instagram" target="_blank"></a>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'vuestic-profile-card',
    props: ['photoSource', 'name', 'location', 'social']
  }
</script>

<style lang="scss">
  $vuestic-profile-card-width: 12.6875rem;
  $vuestic-profile-card-photo-diameter: 9.375rem;

  .vuestic-profile-card {
    width: $vuestic-profile-card-width;
    .photo {
      height: $vuestic-profile-card-photo-diameter;
      width: $vuestic-profile-card-photo-diameter;
      border-radius: 50%;
      background-color: $lighter-gray;
      overflow: hidden;

      img {
        height: 100%;
        width: 100%;
      }
    }
    .name {
      margin-top: 1.325rem;
      margin-bottom: 0;
    }
    .location {
      margin-top: 0.8125rem;
      .icon {
        color: $lighter-gray;
        font-size: $font-size-larger;
      }
      &:hover {
        cursor: pointer;
        .icon {
          color: red;
        }
      }
    }
    .social {
      display: flex;
      justify-content: center;
      padding-top: 1rem;
      margin-top: 1.25rem;
      width: 100%;
      border-top: solid .125rem $light-gray;
      .icon {
        color: $gray;
        text-decoration: none;
        font-size: $font-size-h4;
        margin-right: .4375rem;
        margin-left: .4375rem;
        &:hover {
          cursor: pointer;
          color: darken($gray, 50%);
        }
      }
    }
  }
</style>
