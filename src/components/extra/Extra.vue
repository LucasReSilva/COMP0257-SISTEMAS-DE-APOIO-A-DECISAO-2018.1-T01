<template>
  <div class="extra">
    <vuestic-widget :headerText="'extra.tabs.title' | translate" class="no-v-padding">
      <vuestic-tabs class="tabs" :names="[$t('extra.tabs.setupProfile'), $t('extra.tabs.overview')]">
        <div :slot="'extra.tabs.overview' | translate" class="d-flex justify-content-center">
          <overview-tab></overview-tab>
        </div>
        <div :slot="'extra.tabs.setupProfile' | translate" class="d-flex justify-content-center">
          <setup-profile-tab wizardType="simple"></setup-profile-tab>
        </div>
      </vuestic-tabs>
    </vuestic-widget>

    <div class="row">
      <div v-for="item in contatos" :key="item.id" class="col-md-3 d-flex">
        <vuestic-widget :headerText="$t('extra.profileCard')" class="profile-card-widget">
          <vuestic-profile-card :name="item.nome" :location="item.curso" :photoSource="item.photoURL"
                                :social="{linkedin: 'twitter.com', facebook: 'facebook.com',
                                  instagram: 'instagram.com'}">
          </vuestic-profile-card>
        </vuestic-widget>
      </div>
    </div>
  </div>
</template>

<script>
  import OverviewTab from 'components/dashboard/features-tab/FeaturesTab.vue'
  import SetupProfileTab from 'components/dashboard/setup-profile-tab/SetupProfileTab.vue'
  import LeafletMap from 'components/maps/leaflet-maps/LeafletMap.vue'

  export default {
    name: 'extra',
    components: {
      LeafletMap,
      SetupProfileTab,
      OverviewTab
    },
    data () {
      return {
        chatMessages: [
          {
            text: 'Hello! So glad you liked my work. Do you want me to shoot you?',
            yours: false
          },
          {
            text: 'Yeah, that would be cool. Maybe this Sunday at 3 pm?',
            yours: true
          },
          {
            text: 'Sounds great! See you later!',
            yours: false
          },
          {
            text: 'Should I bring a lightbox with me?',
            yours: true
          },
          {
            text: 'No, thanks. There is no need. Can we set up a meeting earlier?',
            yours: false
          },
          {
            text: 'I\'m working on Vuestic, so let\'s meet at 3pm. Thanks!',
            yours: true
          }
        ],
        posts: [
          {
            name: 'Irina Myatelskaya',
            text: 'joined the network',
            photoURL: 'http://i.imgur.com/VuTDC8u.png'
          },
          {
            name: 'Andrei Hrabouski',
            text: 'has just started a live video',
            photoURL: 'http://i.imgur.com/W3mGrmW.png'
          },
          {
            name: 'Evan You',
            text: 'joined the network',
            photoURL: 'http://i.imgur.com/D7DOGBH.jpg'
          }
        ],
        news: [
          {
            photoURL: 'http://i.imgur.com/PiTDDcA.png'
          },
          {
            photoURL: 'http://i.imgur.com/M6GugaM.png'
          },
          {
            photoURL: 'http://i.imgur.com/vEy3fRU.png'
          },
          {
            photoURL: 'http://i.imgur.com/Xrywphx.png'
          },
          {
            photoURL: 'http://i.imgur.com/dqVtQGY.png'
          },
          {
            photoURL: 'http://i.imgur.com/qP7rTCy.png'
          },
          {
            photoURL: 'http://i.imgur.com/6YLsM43.png'
          },
          {
            photoURL: 'http://i.imgur.com/9PAOx55.png'
          },
          {
            photoURL: 'http://i.imgur.com/mVpc04D.png'
          },
          {
            photoURL: 'http://i.imgur.com/WdbTSLn.png'
          },
          {
            photoURL: 'http://i.imgur.com/ZXRIHfk.png'
          }
        ],
        contatos: [
          {
            id: 1,
            nome: 'Airton Matheus Cardoso Leite',
            curso: 'Ciência da Computação',
            linkedin: 'urlDOIDA',
            email: 'igor.vc30@gmail.com',
            photoURL: 'https://pbs.twimg.com/profile_images/983788544551505921/9xTtNQds_400x400.jpg'
          },
          {
            id: 2,
            nome: 'Gilliard de Jesus Santos',
            curso: 'Ciência da Computação',
            linkedin: 'urlDOIDA',
            email: 'igor.vc30@gmail.com',
            photoURL: 'https://s2.glbimg.com/1g60nFn3dZCY3pt96AlQISrKUWc=/0x0:452x462/1600x0/smart/filters:strip_icc()/s.glbimg.com/es/ge/f/original/2018/07/02/mascote.png'
          },
          {
            id: 3,
            nome: 'Igor Vasconcelos Costa',
            curso: 'Sistemas de Informacao',
            linkedin: 'urlDOIDA',
            email: 'igor.vc30@gmail.com',
            photoURL: 'http://spb2018.com/media/20180630savoia.jpg'
          },
          {
            id: 4,
            nome: 'Lucas Renato Aragão Silva',
            curso: 'Ciência da Computação',
            linkedin: 'urlDOIDA',
            email: 'igor.vc30@gmail.com',
            photoURL: 'https://p2.trrsf.com/image/fget/cf/940/0/images.terra.com/2018/06/16/2662968-cabelo-loiro-de-neymar-prestes-a-jogar-650x488-3.jpg'
          }
        ]

      }
    }
  }
</script>

<style lang="scss" scoped>
  .tabs {
    .overview-tab {
      .explore-row {
        display: none !important;
      }
    }

    .maps-tab {
      height: 500px;
    }
  }

  .profile-card-widget, .chat-widget {
    width: 100%;
    .widget-body {
      display: flex;
      justify-content: center;
      align-items: center;
      & > div {
        width: 100%;
      }
    }
  }

  .bottom-widgets {
    > div[class^='col'] {
      & > div {
        width: 100%;
      }
    }
  }
</style>
