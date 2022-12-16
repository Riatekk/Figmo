<template>
  <div class="container" :style="{width: containerWidth + 'px' }">
    <div class="open-close">
      <i v-if="containerOpen" class="material-icons" @click="toggleContainerState">chevron_left</i>
      <i v-if="!containerOpen" class="material-icons" @click="toggleContainerState">chevron_right</i>
    </div>
    <div style="margin-top: 20px; display: flex; align-items: center; gap: 3px;">
      <img src="../assets/figmo-logo.png" style="width: 25px"/>
      <h2>igmo</h2>
    </div>
   
    <div v-if="containerOpen" class="row">
      <div v-if="activePage" class="col-sm">
        <div v-for="menuItem in menuItems" :key="menuItem.name">
          <h2>{{ menuItem.name }}</h2>

          <ul>
            <li v-for="item in menuItem.items" :key="item.name" @click="createWidget(item.type)">
              <div class="icon-holder">
                <i v-if="item.iconName" class="material-icons">{{item.iconName}}</i>
                <span v-else :class="item.iconName" class="icon-text">{{ item.iconText }}</span>
              </div>

              <span class="icon-label">{{ item.label }}</span>
            </li>
          </ul>
        </div>
      </div>
      <div v-else class="col-sm">
        <h2>select a page</h2>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data () {
      return {
        containerOpen: true,
        menuItems: [{
          name: 'Formulaire',
          items: [{
            iconName: 'check_circle',
            label: 'Bouton',
            type: 'button'
          },{
            iconName: 'check_box',
            label: 'Checkbox',
            type: 'checkbox'
          },{
            iconName: 'arrow_drop_down_circle',
            label: 'Dropdown',
            type: 'dropdown'
          },{
            iconName: 'settings_ethernet',
            label: 'Scrollbar',
            type: 'scrollbar'
          },{
            iconName: 'radio_button_checked',
            label: 'Radio',
            type: 'radio'
          },{
            iconName: 'I',
            label: 'Input',
            type: 'input'
          },{
            iconName: 'remove',
            label: 'Ligne',
            type: 'hr'
          }]
        },{
          name: 'Typography',
          items: [{
            iconName: 'H',
            label: 'Titre',
            type: 'heading'
          },{
            iconName: 'T',
            label: 'Text',
            type: 'label'
          },{
            iconName: 'list',
            label: 'Liste',
            type: 'list'
          }]
        },{
          name: 'Contenu',
          items: [{
            iconName: 'photo',
            label: 'Image',
            type: 'image'
          },{
            iconName: 'lens',
            label: 'Shape',
            type: 'shape'
          },{
            iconName: 'video',
            label: 'Video',
            type: 'video'
          }
        ]
        },{
          /*name: 'other',
          items: [{
            iconName: 'computer',
            label: 'browser',
            type: 'browser'
          },{
            iconName: 'phone_android',
            label: 'mobile',
            type: 'mobile'
          }]*/
        }]
      }
    },

    computed: {
      containerWidth () {
        let width = 290

        if (!this.containerOpen) {
          width = 32
        }

        return width
      },

      activePage () {
        return this.$store.getters.activePage
      }
    },

    methods: {
      createWidget (type) {
        // this.$store.dispatch('createWidget', type)

        var widget = {
          type: type
        }

        switch (type) {
          case 'button':
            Object.assign(widget, {
              w: 120,
              h: 40,
              bc: '#ffffff',
              t: 'button',
              a: 'center'
            });
            break;
          case 'checkbox':
            Object.assign(widget, {
              w: 140,
              h: 40,
              d: [{n: 'checbox', c: true}]
            });
            break;
          case 'dropdown':
            Object.assign(widget, {
              w: 160,
              h: 40,
              bc: '#ffffff',
              t: 'dropdown',
              a: 'left'
            });
            break;
          case 'scrollbar':
            Object.assign(widget, {
              w: 160,
              h: 32,
              bc: '#ffffff'
            });
            break;
          case 'radio':
            Object.assign(widget, {
              w: 140,
              h: 40,
              a: 'left',
              d: [{n: 'radio', c: true}]
            });
            break;
          case 'list':
            Object.assign(widget, {
              w: 140,
              h: 40,
              a: 'left',
              d: [{n: 'item 1'}, {n: 'item 2'}, {n: 'item 3'}]
            });
            break;
          case 'input':
            Object.assign(widget, {
              w: 180,
              h: 40,
              t: 'Label',
              a: 'left',
              c: '#000000',
              bc: '#ffffff'
            });
            break;
          case 'hr':
            Object.assign(widget, {
              w: 180,
              h: 20,
              c: '#000000'
            });
            break;
          case 'heading':
            Object.assign(widget, {
              w: 180,
              h: 40,
              t: 'Heading',
              a: 'left',
              f: '28',
              c: '#000000'
            });
            break;
          case 'label':
            Object.assign(widget, {
              w: 100,
              h: 30,
              t: 'Label',
              a: 'left',
              c: '#000000',
              bc: 'auto'
            });
            break;
          case 'image':
            Object.assign(widget, {
              w: 100,
              h: 100,
              bc: '#ffffff',
              l: ''
            });
            break;
          case 'shape':
            Object.assign(widget, {
              w: 200,
              h: 200,
              bc: '#e1e1e1',
              s: 'rectangle'
            });
            break;
          case 'browser':
            Object.assign(widget, {
              w: 300,
              h: 300,
              bc: '#ffffff',
              z: 0,
              t: 'http://'
            });
            break;
          case 'mobile':
            Object.assign(widget, {
              w: 230,
              h: 340,
              bc: '#ffffff',
              z: 0
            });
            break;
        }

        this.$store.dispatch('createWidget', widget)
      },

      toggleContainerState () {
        const containerState = !this.containerOpen
        this.containerOpen = containerState

        localStorage.setItem('sideSelectorState', containerState)
      }
    },

    created () {
      const containerState = localStorage.getItem('sideSelectorState')

      if (!containerState) {
        return
      }

      this.containerOpen = JSON.parse(containerState)
    }
  }
</script>

<style lang="scss" scoped>

  @import '../styles/_main.scss';

  .container {
    position: fixed;
    top: 50%;
    transform: translateY(-50%);
    left: 0;
    height: 90%;
    border-radius: 0 20px 20px 0;
    background-color: $sidebar-background-color;
    z-index: 1000;
    color: $sidebar-color;
  }

  .open-close {
    position: absolute;
    top: 20px;
    right: 5px;
    color: $sidebar-color;
    z-index: 1;
    cursor: pointer;
  }

  .row {
    padding-top: 10px;

    h2 {
      margin: 10px 0 15px 0;
    }

    ul {
      list-style: none;
      margin: 0;
      padding: 0;

      li {
        display: inline-block;
        text-align: center;
        width: 84px;
        margin: 0 2px 10px 0;
        padding: 15px 0 5px 0;
        min-height: 66px;
        position: relative;

        background-color: $sidebar-icon-background-color;
        border-radius: 20px;
        transform: scale(0.9);

        .icon-holder {
          height: 40px;
          font-size: 2.6rem;
          line-height: 2.8rem;
          color: $sidebar-icon-color-primary;

          .icon-text {
            font-style: italic;
            font-size: 2.6rem;
          }
        }

        &:hover {
          box-shadow: 0 0 8px $sidebar-icon-background-color-hover;
          cursor: pointer;
        }
      }
    }
  }

</style>
