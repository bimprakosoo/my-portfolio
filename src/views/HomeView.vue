<template>
  <v-app id="home">
    <NavBar/>
    <v-container fluid>
      <div class="head">
        <v-row>
          <v-col cols="6">
            <div style="position: relative" class="mt-16">
              <h1 class="text-grey">Hello,</h1>
              <h1 class="text-white">I'm Bimo Prakoso</h1>
              <span class="text-grey">Backend Developer</span><br/>
              <v-btn tile dark class="text-yellow mt-8" variant="outlined"><a href="bimo-resume.pdf" download class="text-yellow" style="text-decoration: none">Download CV</a></v-btn>
              <v-btn tile dark class="text-yellow mt-8" variant="outlined" @click="scroll('contact')" style="margin-left: 10px">Contact Me</v-btn>
            </div>
          </v-col>
          <v-col cols="6">
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
              <div class="child">
                <v-img src="nodejs.png" height="50px"></v-img>
                <h3 class="ml-3 mt-4">Node.js</h3>
              </div>
            </v-col>
          </v-row>
          <v-divider></v-divider>
        </div>
      </v-col>
      <v-col cols="12" sm="12" id="portfolio" class="port">
        <div class="text-center mt-4 ">
          <h2>Portfolio</h2>
          <div style="width:120px; margin: 0 auto">
            <v-slider v-model="slider2" color="yellow"></v-slider>
          </div>
        </div>
        <div class="d-flex justify-center mb-6">
          <v-btn :color="getButtonColor('All')" class="mr-2" @click="selectCategory('All')">All</v-btn>
          <v-btn :color="getButtonColor('Web')" class="mr-2" @click="selectCategory('Web')">Web</v-btn>
          <v-btn :color="getButtonColor('Game')" class="mr-2" @click="selectCategory('Game')">Game</v-btn>
          <v-btn :color="getButtonColor('Discord')" class="mr-2" @click="selectCategory('Discord')">Discord Bot</v-btn>
        </div>
      </v-col>
      <v-dialog v-model="dialog" max-width="1000px" class="img-port">
        <v-card>
          <v-carousel hide-delimiters v-model="carouselIndex" style="height: 800px !important">
            <v-carousel-item v-for="(item, index) in carouselItems" :key="index" style="display: flex">
              <div>
                <v-img :src="item.img" height="600px" contain></v-img>
                <div class="text-description">{{ item.description }}</div>
                <div class="text-framework">{{ item.framework }}</div>
                <div class="text-url"><a :href="item.url" target="_blank">Check Github / Link Project</a></div>
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
          <v-btn v-if="filteredItems.length >= 6" color="#FBDF7E" class="mt-4" @click="loadMore">Load More</v-btn>
        </div>
      </v-col>
      <v-col cols="12" id="contact">
        <div class="hire">
          <v-row>
            <v-col cols="12" sm="10">
              <h1 class="mt-9 text-white">Hire me for your awesome project</h1>
              <p class="text-grey">
                If you are interested in collaborating with me, please contact me via email.
              </p>
            </v-col>
            <v-col cols="12" sm="2">
              <a :href="'mailto:biimoprakosoo@gmail.com'" class="mt-15">
                <v-btn color="#FBDF7E" class="mt-15">Hire Me</v-btn>
              </a>
            </v-col>
          </v-row>
        </div>
      </v-col>
      <div class="social-icons">
        <v-btn icon href="https://gitlab.com/bimprakosoo" style="margin-bottom: 20px" target="_blank">
          <v-icon icon="fa-brands fa-gitlab"></v-icon>
        </v-btn>
        <v-btn icon href="https://github.com/bimprakosoo" style="margin-bottom: 20px" target="_blank">
          <v-icon icon="fa-brands fa-github"></v-icon>
        </v-btn>
        <v-btn icon href="https://www.linkedin.com/in/bimooprakosoo/" target="_blank">
          <v-icon icon="fa-brands fa-linkedin"></v-icon>
        </v-btn>
      </div>
    </v-container>
  </v-app>
</template>

<script>
import { defineComponent } from 'vue';
import ScrollReveal from "scrollreveal";

// Components
import NavBar from "@/components/NavBar.vue";

export default defineComponent({
  name: 'HomeView',
  mounted() {
    const sr = ScrollReveal();

    sr.reveal('.head', {origin: 'top', distance: '20px', duration: 1000});
    sr.reveal('.padd', {origin: 'bottom', distance: '20px', duration: 1000});
    sr.reveal('.port', {origin: 'left', distance: '20px', duration: 1000});
    sr.reveal('.imgHover', {origin: 'right', distance: '20px', duration: 1000});
    sr.reveal('.hire', {origin: 'bottom', distance: '20px', duration: 1000});

    this.visibleItems = this.items.slice(0, this.loadCount);
  },
  data() {
    return {
      slider2: 50,
      items: [
        { img: "haloteach.png", category : "Web", description: '\n' +
            'Haloteach is a website where teachers and students can engage in online learning. For teachers, there are several features such as creating classes for students to choose from, creating quizzes, ' +
            'and uploading learning materials. As for students, they can select classes they want to take, participate in quizzes provided by teachers, access free materials from the classes they enroll in, and provide ratings for ' +
            'teachers/classes they attend. Additionally, Haloteach collaborates with external tutoring services that wish to enter the world of online learning.',
          framework: "Built with Codeigniter And MySQL", url: ""
        },
        { img: "halokes.png", category : "Web", description: '\n' +
            'Halokes is a website/application for school administration. In this system, the school can perform various tasks such as managing class schedules, the latest curriculum, teacher/student attendance, extracurricular activities, ' +
            'and more. On the other hand, students can submit assignments, view their grade history from past semesters, or check their attendance records.',
          framework: "Built with Codeigniter and MySQL", url: ""
        },
        { img: "nitromax.png", category : "Web", description: 'Nitromax is a system designed to monitor nitrogen filling stations commonly found at gas stations. In addition to nitrogen filling, the system allows users to view sales data, such as tire repair transactions, ' +
            'oil sales, tire replacement services, and more. Clients can perform various tasks on the Nitromax website, such as viewing sales data, modifying prices for goods/services, adding new services/products, monitoring operator attendance, and more. In addition to the website, ' +
            'Nitromax utilizes a mobile application to connect the nitrogen machine to the Nitromax system.',
          framework: "Built with Codeigniter and MySQL", url: ""
        },
        { img: "autoglaze.png", category : "Web", description: 'Autoglaze is a POS system for car wash and other transactions. The application utilizes a mobile app and a website to monitor car wash transactions. The car wash service provider can perform various ' +
            'actions using the application, such as inputting the car license plate, selecting services chosen by customers, adding desired extras, and more. Additionally, through the website system, the car wash service provider can monitor sales data, add new products/services, ' +
            'modify prices, create vouchers and promotions, and perform other related tasks.',
          framework: "Built with Laravel and MySQL", url: ""
        },
        { img: "united_tractor.png", category : "Web", description: 'United Tractor is a website designed to monitor construction projects undertaken by United Tractor. It offers several features such as financial expense management, progress tracking for each construction project, a directory system, ' +
            'geolocation services, and more.',
          framework: "Built with Codeigniter and MySQL", url: ""
        },{ img: "track-task.png", category : "Web", description: 'A simple trello clone to track your task.',
          framework: "Built with Next.js, React Drag and Drop, and Firebase", url: "https://simple-trello-theta.vercel.app/"
        },
        { img: "article-summarize.png", category : "Web", description: 'A simple application to summarize articles.',
          framework: "Built with React.js, Vite, Tailwind.css, Redex, and RapidAPI", url: "https://article-summarize.vercel.app/"
        },
        { img: "jeruk_emas.png", category : "Game", description: 'Jeruk Emas is a Unity-based game where the player\'s objective is to find the golden orange while avoiding enemy pursuit. The enemy objects utilize two algorithms to chase the player. The first algorithm is A*, which finds the fastest path to the player. ' +
            'The second algorithm is FSM (Finite State Machine), which has multiple states for chasing the player.',
          framework: "Built with Unity", url: ""
        },
        { img: "link-changer.png", category : "Discord", description: 'A Discord Bot that has function to automatically modified url video from twitter, tiktok, and instagram so it can be played on discord without click the link because sometimes those url ' +
            'got error and can not be played. It is using existing library from other people github, so the bot only change the url.',
          framework: "Built with Node.js with discord.js plugin", url: "https://github.com/bimprakosoo/link-changer-bot"
        },
        { img: "chatgpt.png", category : "Discord", description: 'A Discord Bot that can answer your question like chatGPT. Using gpt 3.5 as a model for this bot, now you can ask anything in your server.',
          framework: "Built with Node.js with discord.js and openai", url: "https://github.com/bimprakosoo/chatGPT-bot"
        },
      ],
      loadCount: 6,
      selectedCategory : 'All',
      dialog: false,
      selectedItem: null,
      carouselIndex: 0,
    };
  },
  computed: {
    filteredItems() {
      if (this.selectedCategory === 'All') {
        return this.items.slice(0, this.loadCount);
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
    visibleItems() {
      return this.filteredItems.slice(0, 6);
    }
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
    scroll(refName) {
      const element = document.getElementById(refName);
      element.scrollIntoView({behavior: "smooth"});
    },
    loadMore() {
      this.loadCount += 6;
      this.visibleItems = this.items.slice(0, this.loadCount);
    }
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
 }
.head:before {
  content: " ";
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: 50%;
  background: #262A56;
  transform: skew(0deg, 6deg);
}
.head:after {
  content: " ";
  position: absolute;
  top: 0;
  right: 0;
  height: 100%;
  width: 50%;
  background: #262A56;
  transform: skew(0deg, -6deg);
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
.hire {
  width: 100%;
  height: 200px;
  padding: 0 200px;
  background-color: #262A56;
  margin-top: -24px;
}
.text-description {
  padding: 16px;
  font-size: 16px;
  text-align: justify;
}
.text-framework {
  padding: 16px;
  font-size: 18px;
  text-align: center;
}
.text-url {
  padding: 16px;
  font-size: 18px;
  text-align: center;
}
a:link {
  color: #000000;
}
a:visited {
  color: #000000;
}
.social-icons {
  position: fixed;
  bottom: 20px; /* Adjust the bottom position as needed */
  left: 20px; /* Adjust the left position as needed */
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}
</style>
