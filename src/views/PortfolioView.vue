<template>
  <div class="system" id="system">
    <div class="container">
      <div class="row">
        <div class="col-12">
          <h3 class="main_title">作品集</h3>
        </div>
        <div class="col-12 web_tab">
          <!-- tab標籤列 -->
          <ul>
            <li
              :class="{ active: tab.name === tabID }"
              @click="changeTab(tab.name)"
              v-for="tab in tabNav"
              :key="tab"
              class="pro_btn"
            >
              <a>{{ tab.tabname }}</a>
            </li>
          </ul>
          <!-- tab內容 -->
          <div class="web_flex">
            <div
              class="web_proBox fade-in-bottom"
              v-for="item in filtered"
              :key="item"
              :class="item.value"
              @click="ClickPopUp(item.id)"
            >
              <div class="web_box" v-on:click="modalopen" :id="item.id">
                <div class="web_img"><img :src="item.img" /></div>
                <div class="web_type">
                  <span>{{ item.subText }}</span>
                </div>
              </div>
              <div class="web_txt">
                <p class="mt-3">{{ item.text }}</p>
              </div>
            </div>
            <!-- modal -->
            <div v-for="system in system" :key="system.id">
              <div
                class="modal"
                :class="{ show: system.isShow }"
                :id="system.id"
              >
                <div>
                  <h5 class="page_title">{{ system.title }}</h5>
                  <div class="sys_page">
                    <div class="sys_pageImg">
                      <img :src="system.img" />
                    </div>
                    <div class="sys_pageText">
                      <p><strong>系統概述</strong></p>
                      <p v-html="system.text"></p>
                    </div>
                    <div class="sys_pageImg">
                      <h3>002</h3>
                      <img :src="system.img" />
                    </div>
                    <div class="sys_pageImg">
                      <h3>003</h3>
                      <img :src="system.img" />
                      <p v-html="system.text"></p>
                    </div>
                  </div>
                  <button v-on:click="system.isShow = false" class="close_btn">
                    <p>X</p>
                    <!-- <i class="icon-close">X</i> -->
                  </button>
                </div>
              </div>
              <div class="bg" v-bind:class="{ show: system.isShow }"></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.web_flex {
  display: flex;
  flex-wrap: wrap;
}
.web_flex .web_proBox {
  width: calc(100% / 3 - 2rem);
  margin: 1rem;
}
.web_tab ul {
  display: flex;
  flex-wrap: wrap;
  list-style: none;
  padding-left: 0;
}
.web_tab ul li {
  cursor: pointer;
}
.web_txt {
  margin: 1rem;
  margin-top: 0;
  border-left: 1px solid #3d3d3d;
  padding-left: 1rem;
  padding-top: 0.2rem;
}
.pro_btn.active {
  background: var(--mainColor);
  color: #fff;
}
.web_box {
  position: relative;
  cursor: pointer;
}
.web_box .web_img {
  overflow: hidden;
}
.web_box .web_img img {
  transition: all 0.5s ease-out;
}
.web_box:hover .web_type {
  opacity: 1;
}
.web_box:hover .web_img {
  position: relative;
}
.web_box:hover .web_img img {
  transform: scale(1.05);
}
.web_box:hover .web_img::after {
  content: "";
  background: white;
  /* Old browsers */
  background: -moz-linear-gradient(top, rgba(255, 255, 255, 0) 0%, #444 100%);
  /* FF3.6-15 */
  background: -webkit-linear-gradient(
    top,
    rgba(255, 255, 255, 0) 0%,
    #444 100%
  );
  /* Chrome10-25,Safari5.1-6 */
  background: linear-gradient(to bottom, rgba(255, 255, 255, 0) 0%, #444 100%);
  /* W3C, IE10+, FF16+, Chrome26+, Opera12+, Safari7+ */
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#ffffff', endColorstr='#444444',GradientType=0);
  /* IE6-9 */
  width: 100%;
  height: 50%;
  position: absolute;
  bottom: 0;
  left: 0;
}
.web_type {
  position: absolute;
  bottom: 15px;
  right: 15px;
  color: #fff;
  opacity: 0;
  transition: 0.5s;
}
.modal {
  display: block;
  box-sizing: border-box;
  position: fixed;
  top: 0;
  bottom: 0;
  right: 0;
  left: 0;
  z-index: 1001;
  width: 90%;
  height: 85vh;
  margin: auto;
  padding: 30px;
  border: 1px solid #eee;
  border-radius: 15px;
  background-color: #fff;
  text-align: center;
  visibility: hidden;
  opacity: 0;
  -webkit-transition: 0.2s;
  transition: 0.2s;
  background: #fff;
  background-size: 60%;
}
.bg {
  display: block;
  position: fixed;
  bottom: 0;
  left: 0;
  z-index: 1000;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.6);
  visibility: hidden;
  opacity: 0;
  -webkit-transition: 0.3s;
  transition: 0.3s;
}
.show {
  visibility: visible;
  opacity: 1;
}
.page_title {
  color: var(--thirdcolor);
  font-size: 1.75rem;
  font-weight: bold;
  margin: 1rem;
}
.sys_page {
  display: flex;
  justify-content: space-around;
}
.sys_page .sys_pageImg {
  width: 40%;
  margin: 3rem;
}
.sys_page .sys_pageImg img {
  border-radius: 15px;
  box-shadow: 5px 5px 5px var(--shodowColor);
}
.sys_page .sys_pageText {
  width: 50%;
  text-align: left;
  margin-top: 3rem;
}
button.close_btn {
  background: #fff;
  border: none;
  position: absolute;
  right: 3rem;
  top: 3rem;
}
button.close_btn i {
  color: var(--black);
  font-size: 1.75rem;
  font-weight: bold;
}
button.close_btn:hover i {
  color: var(--maincolor);
}

@media screen and (max-width: 1199px) {
  button.close_btn {
    right: 1rem;
    top: 1rem;
  }
  .sys_page {
    flex-wrap: wrap;
  }
  .sys_page .sys_pageImg {
    width: 100%;
    margin: 1rem 0;
  }
  .sys_page .sys_pageText {
    width: 100%;
    margin-top: 2rem;
  }
}
@media screen and (max-width: 991px) {
  .web_flex .web_proBox {
    width: calc(100% / 2 - 2rem);
  }
}
@media screen and (max-width: 767px) {
  .web_flex .web_proBox {
    width: 100%;
  }
  .page_title {
    font-size: 1.5rem;
  }
}
</style>

<script>
export default {
  data() {
    return {
      tabID: "All",
      tabNav: [
        {
          name: "All",
          tabname: "All",
        },
        {
          name: "csc",
          tabname: "中鋼專區",
        },
        {
          name: "countrycom",
          tabname: "國營企業",
        },
        {
          name: "ec",
          tabname: "環保化學",
        },
        {
          name: "medi",
          tabname: "媒體傳播",
        },
        {
          name: "metal",
          tabname: "金屬工業",
        },
        {
          name: "chain",
          tabname: "連鎖體系",
        },
        {
          name: "trans",
          tabname: "交通運輸",
        },
        {
          name: "text",
          tabname: "紡織工業",
        },
      ],
      category: [
        {
          img: "",
          text: "中鋼人力資源資訊系統",
          subText: "中鋼專區",
          link: "",
          value: ["All", "csc"],
          id: "01",
        },
        {
          img: "",
          text: "CRM系統/會員管理系統",
          subText: "連鎖體系",
          link: "",
          value: ["All", "chain"],
          id: "02",
        },
      ],
      // 彈出視窗
      isShow: false,
      system: [
        {
          title: "中鋼人力資源資訊系統",
          img: "1111111",
          text: `<div>1233</div>
          <hr>
          <p>中鋼內部員工人事、請假、薪資與教育訓練等人力資訊相關之查詢系統。</p>
          <div>
            <h2>123321</h2>  
            <h2>123321</h2>  
            <h2>123321</h2>  
            <h2>123321</h2>  
            <h2>123321</h2>  
            <h2>123321</h2>  
            <h2>123321</h2>  
          </div>
          `,
          id: "01",
          isShow: false,
        },
        {
          title: "CRM系統/會員管理系統",
          img: "222222",
          text: "會員資料管理系統，記錄客戶所購買的產品、分類客戶類型，依客戶群舉辦活動",
          id: "02",
          isShow: false,
        },
      ],
    };
  },

  methods: {
    changeTab(id) {
      this.tabID = id;
    },
    ClickPopUp(id) {
      for (let i = 0; i < this.system.length; i++) {
        if (this.system[i].id === id) {
          this.system[i].isShow = true;
        } else {
          this.system[i].isShow = false;
        }
      }
    },
  },

  computed: {
    filtered() {
      return this.category.filter((item) => item.value.includes(this.tabID));
    },
  },
};
</script>
