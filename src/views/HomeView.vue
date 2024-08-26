<template>
  <div>
    <h1>Hello World</h1>
    <button style="font-size: 3rem;" @click="login">Login</button>
    <button style="font-size: 3rem;" @click="action">SetItem</button>
    <button style="font-size: 3rem; margin-left: 1rem" @click="check">Check</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // userData: {
      //   localname: 'Site ID',
      //   localurl: 'siteid',
      //   locatorname: 'Search ID',
      //   locatorurl: 'searchid',
      //   enhancename: 'Enhance ID',
      //   enhanceurl: 'enhanceid'
      // },
      sidebarMenuRoot: {
        local: {
          name: 'Site ID',
          url: 'siteid'
        },
        locator: {
          name: 'Search ID',
          url: 'searchid'
        },
        // enhance: {
        //   name: 'Enhance ID',
        //   url: 'enhanceid'
        // }
      },
    }
  },

  // mounted() {
  //   this.action();
  // },  

  methods: {
    login() {
      if(typeof this.sidebarMenu === 'undefined') {
        console.log('block1');
        localStorage.setItem('userData', JSON.stringify({
          localname: this.sidebarMenuRoot.local.name,
          localurl: this.sidebarMenuRoot.local.url,
          locatorname: this.sidebarMenuRoot.locator.name,
          locatorurl: this.sidebarMenuRoot.locator.url,
          enhancename: this.sidebarMenuRoot.enhance ? this.sidebarMenuRoot.enhance.name : '',
          enhanceurl: this.sidebarMenuRoot.enhance ? this.sidebarMenuRoot.enhance.url : '',
        }));
      } else {
        console.log('block2');
        localStorage.setItem('userData', JSON.stringify({
          localname: this.sidebarMenu.local.name,
          localurl: this.sidebarMenu.local.url,
          locatorname: this.sidebarMenu.locator.name,
          locatorurl: this.sidebarMenu.locator.url,
          enhancename: this.sidebarMenu.enhance.name,
          enhanceurl: this.sidebarMenu.enhance.url
        }));
      }
    },

    action() {
      // cek apakah enhancename atau url kosong
      if(typeof this.sidebarMenuRoot.enhance === 'undefined' || typeof this.sidebarMenuRoot.enhance === 'undefined') {
        console.log('block4');
        let _userData = JSON.parse(localStorage.getItem('userData'));

        // maka hapus enhancename dan enhanceurl dari local storage jika ada
        if(_userData.enhancename !== "" || _userData.enhanceurl !== "") {
          console.log("block4");
          _userData.enhancename = "";
          _userData.enhanceurl = "";
          localStorage.setItem('userData', JSON.stringify(_userData));
        }
      }
      // cekapakah enhancename dan url ada
      else {
        let _userData = JSON.parse(localStorage.getItem('userData'));

        // maka tambahkan enhancename dan enhanceurl dari localstorage jika belum ada
        if(_userData.enhancename === "" || _userData.enhanceurl === "") {
          console.log("block2");
          _userData.enhancename = this.sidebarMenuRoot.enhance.name;
          _userData.enhanceurl = this.sidebarMenuRoot.enhance.url;
          localStorage.setItem('userData', JSON.stringify(_userData));
        }
      }




      // localStorage.setItem('userData', JSON.stringify(this.userData));
    },

    check() {
      console.log(this.userData.enhancename === undefined);
      console.log(this.userData.enhanceurl === undefined);
    }
  }
}
</script>