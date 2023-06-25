<template>
  <v-app id="home">
    <NavBar/>
    <v-container fluid>
      <div class="head">
        <v-row>
          <v-col cols="5">
            <div style="position: relative" class="mt-16">
              <h1 class="text-grey">Hello,</h1>
              <h1 class="text-white">I'm Bimo Prakoso</h1>
              <span class="text-grey">Backend Developer</span><br/>
              <v-btn tile dark class="text-yellow mt-8" variant="outlined">Download CV</v-btn>
            </div>
          </v-col>
          <v-col cols="2">
            <div style="
                position: absolute;
                z-index: 9999;
                bottom: 0;
                margin-left: auto;
                margin-right: auto;
                left: 0;
                right: 0;
                text-align: center;
              " class="mt-16">
              <v-icon>fas fa-angle-double-down</v-icon>
            </div>
          </v-col>
          <v-col cols="5">
            <div style="position: relative; z-index: 9999" class="mt-16">
              <v-img src="avatar.png" contain max-height="300"></v-img>
            </div>
          </v-col>
        </v-row>
      </div>
      <div class="text-center mt-16">
        <h2>Skill</h2>
        <div style="width:120px; margin: 0 auto">
          <v-slider v-model="slider2" color="yellow"></v-slider>
        </div>
      </div>
      <v-col cols="12" class="padd" id="skill">
        <div class="first" id="project">
          <v-row>
            <v-col cols="12">
              <div class="child">
                <v-img src="laravel.png" height="50px"></v-img>
                <h3 class="ml-3 mt-4">Laravel</h3>
              </div>
              <div class="child">
                <v-img src="codeigniter.png" height="50px"></v-img>
                <h3 class="ml-3 mt-4">Codeigniter</h3>
              </div>
              <div class="child">
                <v-img src="rest-api.png" height="50px"></v-img>
                <h3 class="ml-3 mt-4">RestAPI</h3>
              </div>
              <div class="child">
                <v-img src="mysql.png" height="50px"></v-img>
                <h3 class="ml-3 mt-4">MySQL</h3>
              </div>
              <div class="child">
                <v-img src="vue.png" height="50px"></v-img>
                <h3 class="ml-3 mt-4">Vue.js</h3>
              </div>
              <div class="child">
                <v-img src="git.png" height="50px"></v-img>
                <h3 class="ml-3 mt-4">GIT</h3>
              </div>
              <div class="child">
                <v-img src="javascript.png" height="50px"></v-img>
                <h3 class="ml-3 mt-4">Javascript</h3>
              </div>
              <div class="child">
                <v-img src="unity.jpg" height="50px"></v-img>
                <h3 class="ml-3 mt-4">Unity</h3>
              </div>
            </v-col>
          </v-row>
          <v-divider></v-divider>
        </div>
      </v-col>
      <v-col cols="12" sm="12" id="portfolio">
        <div class="text-center mt-4">
          <h2>Portfolio</h2>
          <div style="width:120px; margin: 0 auto">
            <v-slider v-model="slider2" color="yellow"></v-slider>
          </div>
        </div>
        <div class="d-flex justify-center mb-6">
          <v-btn :color="getButtonColor('All')" class="mr-2" @click="selectCategory('All')">All</v-btn>
          <v-btn :color="getButtonColor('Web')" class="mr-2" @click="selectCategory('Web')">Web</v-btn>
          <v-btn :color="getButtonColor('Web')" class="mr-2" @click="selectCategory('Game')">Game</v-btn>
        </div>
      </v-col>
      <v-dialog v-model="dialog" max-width="1000px">
        <v-card>
          <v-carousel hide-delimiters v-model="carouselIndex" style="height: auto !important">
            <v-carousel-item v-for="(item, index) in carouselItems" :key="index" style="display: flex">
              <div>
                <v-img :src="item.img" height="600px" contain></v-img>
                <div class="text-description">{{ item.description }}</div>
              </div>
            </v-carousel-item>
          </v-carousel>
        </v-card>
      </v-dialog>
      <v-col cols="12" class="imgHover">
        <v-row class="fill-height" align="center" justify="center">
          <template v-for="(item, i) in filteredItems" :key="i">
            <v-col cols="12" md="4">
              <v-hover v-slot="{ isHovering, props }">
                <v-card :elevation="isHovering ? 12 : 2" :class="{'on-hover': isHovering}" v-bind="props" @click="openModal(item, i)">
                  <v-img :src="item.img" height="225px" cover></v-img>
                </v-card>
              </v-hover>
            </v-col>
          </template>
        </v-row>
      </v-col>
      <v-col cols="12" sm="12">
        <div class="d-flex justify-center mb-6">

        </div>
      </v-col>
      <v-col cols="12" id="biog">
        <div class="hire">
          <v-row>
            <v-col cols="12" sm="8">
              <h1 class="mt-9">Hire me for your awesome project</h1>
              <p class="text-grey">
                Lorem ipsum dolor sit amet consectetur adipisicing elit. Quod
                itaque, eaque molestiae deleniti, earum voluptate eos id dicta
                at, blanditiis
              </p>
            </v-col>
            <v-col cols="12" sm="4">
              <v-btn color="#FBDF7E" class="mt-15">Hire Me</v-btn>
            </v-col>
          </v-row>
        </div>
      </v-col>
      <v-col cols="12" sm="12" class="px-16" id="contact">
        <v-row>
          <v-col cols="12" sm="4">
            <div class="child">
              <h1>Contact info.</h1>
              <v-btn
                icon="fas fa-phone-alt"
                color=""
                class="mt-10"
                variant="outlined"
              ></v-btn
              ><br />
              <span class="text-caption">+6281331398067 </span> <br />
              <v-btn
                icon="fas fa-envelope"
                color=""
                class="mt-10"
                variant="outlined"
              ></v-btn
              ><br />
              <span class="text-caption">biimoprakosoo@gmail.com </span> <br />
            </div>
          </v-col>
          <v-col cols="12" sm="8">
            <h1 class="mt-8">Send your message</h1>
            <v-divider></v-divider>
            <span class="text-caption"
            >Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt
              fugiat officia, odio eaque exercitationem libero nesciunt placeat,
              repellat obcaecati sed tenetur! Est labore aliquam amet
              consequatur necessitatibus fugit obcaecati facilis!</span
            >
            <v-row class="mt-10">
              <v-col cols="12" sm="6">
                <v-text-field
                  label="Name"
                  persistent-hint
                  variant="outlined"
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="6">
                <v-text-field
                  label="Phone No"
                  persistent-hint
                  variant="outlined"
                ></v-text-field>
              </v-col>
            </v-row>
            <v-textarea
              label="Message"
              persistent-hint
              variant="outlined"
            ></v-textarea>
            <v-btn color="#FBDF7E" class="mt-2">Submit Now</v-btn>
          </v-col>
        </v-row>
      </v-col>
    </v-container>
  </v-app>
</template>

<script>
import { defineComponent } from 'vue';

// Components
import NavBar from "@/components/NavBar.vue";

export default defineComponent({
  name: 'HomeView',
  data() {
    return {
      slider2: 50,
      items: [
        { img: "haloteach.png", category : "Web", description: '\n' +
            'Haloteach is a website where teachers and students can engage in online learning. For teachers, there are several features such as creating classes for students to choose from, creating quizzes, ' +
            'and uploading learning materials. As for students, they can select classes they want to take, participate in quizzes provided by teachers, access free materials from the classes they enroll in, and provide ratings for ' +
            'teachers/classes they attend. Additionally, Haloteach collaborates with external tutoring services that wish to enter the world of online learning.' },
        { img: "halokes.png", category : "Web", description: '\n' +
            'Halokes is a website/application for school administration. In this system, the school can perform various tasks such as managing class schedules, the latest curriculum, teacher/student attendance, extracurricular activities, ' +
            'and more. On the other hand, students can submit assignments, view their grade history from past semesters, or check their attendance records.' },
        { img: "nitromax.png", category : "Web", description: 'Nitromax is a system designed to monitor nitrogen filling stations commonly found at gas stations. In addition to nitrogen filling, the system allows users to view sales data, such as tire repair transactions, ' +
            'oil sales, tire replacement services, and more. Clients can perform various tasks on the Nitromax website, such as viewing sales data, modifying prices for goods/services, adding new services/products, monitoring operator attendance, and more. In addition to the website, ' +
            'Nitromax utilizes a mobile application to connect the nitrogen machine to the Nitromax system.' },
        { img: "autoglaze.png", category : "Web", description: 'Autoglaze is a POS system for car wash and other transactions. The application utilizes a mobile app and a website to monitor car wash transactions. The car wash service provider can perform various ' +
            'actions using the application, such as inputting the car license plate, selecting services chosen by customers, adding desired extras, and more. Additionally, through the website system, the car wash service provider can monitor sales data, add new products/services, ' +
            'modify prices, create vouchers and promotions, and perform other related tasks.' },
        { img: "united_tractor.png", category : "Web", description: 'United Tractor is a website designed to monitor construction projects undertaken by United Tractor. It offers several features such as financial expense management, progress tracking for each construction project, a directory system, ' +
            'geolocation services, and more.' },
        { img: "jeruk_emas.png", category : "Game", description: 'Jeruk Emas is a Unity-based game where the player\'s objective is to find the golden orange while avoiding enemy pursuit. The enemy objects utilize two algorithms to chase the player. The first algorithm is A*, which finds the fastest path to the player. ' +
            'The second algorithm is FSM (Finite State Machine), which has multiple states for chasing the player.' },
      ],
      selectedCategory : 'All',
      dialog: false,
      selectedItem: null,
      carouselIndex: 0,
    };
  },
  computed: {
    filteredItems() {
      if (this.selectedCategory === 'All') {
        return this.items;
      } else {
        return this.items.filter((item) => item.category === this.selectedCategory);
      }
    },
    carouselItems() {
      if (this.selectedCategory === 'All') {
        return this.items;
      } else {
        return this.items.filter((item) => item.category === this.selectedItem.category);
      }
    },
  },
  methods: {
    selectCategory(category) {
      this.selectedCategory = category;
    },
    getButtonColor(category) {
      return this.selectedCategory === category ? '#FBDF7E' : '';
    },
    openModal(item, index) {
      this.selectedItem = item;
      this.carouselIndex = index;
      this.dialog = true;
    },
  },
  components: {
    NavBar,
  },
});
</script>
<style scoped>
.v-container {
  padding: 16px 0;
}
.head {
  position: relative;
  text-align: center;
  padding: 12px;
  margin-bottom: 6px;
  height: 400px;
  width: 100%;
  color: white;
 }
.head:before {
  content: " ";
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: 50%;
  background: black;
  transform: skew(0deg, 6deg);
}
.head:after {
  content: " ";
  position: absolute;
  top: 0;
  right: 0;
  height: 100%;
  width: 50%;
  background: black;
  transform: skew(0deg, -6deg);
}
.egg {
  display: block;
  margin-left: 100px;
  margin-top: 50px;
  width: 356px;
  height: 300px;
  background-color: #FBDF7E;
  border-radius: 50% 50% 50% 50% / 60% 60% 40% 0%;
}
.first {
  width: 100%;
  height: 280px;
  text-align: center;
  padding: 2rem 2rem;
}
.child {
  display: inline-block;
  padding: 2rem 1rem;
  vertical-align: middle;
  text-align: center;
  margin-right: 8px;
}
.imgHover {
  padding: 0 200px;
}
.pre {
  width: 100%;
  height: 380px;
  text-align: center;
  padding: 0 200px;
  background-color: #F5F5F5;
}
.hire {
  width: 100%;
  height: 200px;
  padding: 0 200px;
  background-color: #E9E9E9;
  margin-top: -24px;
}
.text-description {
  padding: 16px;
  font-size: 16px;
  text-align: center;
}
</style>
