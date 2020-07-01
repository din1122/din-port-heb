<template>
  <v-container fluid>
    <section class="home">
      <v-layout wrap fill-height>
        <v-flex xl5 lg5 md8 align-end d-flex class="left-home">
          <v-card flat class="home-text-card" style="background:transparent;">
            <div class="d-block">
              <span class="span-title">DIN ASHKENAZI</span>
              <h1>Website</h1>
              <h1>UI UX Desginer</h1>
              <p class="subheading">
                Over the past 6 years, as a desginer and front-end developer,
                I've worked with clients and entrepreneurs to successfully help
                them reach their full potential.
              </p>
              <span>
                <span class="link bolded-span pa-2">
                  <nuxt-link to="/">
                    View Projects
                  </nuxt-link>
                </span>
                or

                <span class="link bolded-span pa-2">
                  <nuxt-link to="/about">
                    Read About me
                  </nuxt-link>
                </span>
              </span>
            </div>
          </v-card>
        </v-flex>
        <v-flex xl7 xs12 md12 lg7 @mouseenter="hover = true" class="right-home">
          <div class="backdrop-img" :class="{ backdropactive: hover }"></div>
          <v-lazy
            :options="{
              threshold: 0.5
            }"
            min-height="200"
            transition="fade-transition"
          >
            <v-img
              class="profile-img"
              src="/photos/profile-pic.png"
            ></v-img>
          </v-lazy>
        </v-flex>
      </v-layout>
    </section>
    <!-- case studies 
     :position="{'20vh center': $vuetify.breakpoint.mdAndDown,'center center ': $vuetify.breakpoint.lgAndUp }"
    -->
    <section pt-5>
      <v-layout wrap>
        <v-flex xl12 xs12>
          <v-card height="300px" class="trans-card" flat align-center>
            <v-card-title class="fill-height">
              <div class="letswork-container">
                <span class="span-title">SELECTED PROJECTS</span>
                <h1>Case studies</h1>
              </div>
            </v-card-title>
          </v-card>
        </v-flex>
        <v-flex xl12>
          <v-layout wrap>
            <CaseStudies
              :key="project.id"
              :id="project.id"
              v-for="project in projects.projects"
              :title="project.title"
              :year="project.year"
              :thumbnail="project.thumbnail"
            ></CaseStudies>
          </v-layout>
        </v-flex>
      </v-layout>
    </section>
    <!-- Personal Projects -->
    <section>
      <v-layout wrap>
        <v-flex xl12 xs12>
          <v-card d-flex height="200px" flat align-center>
            <v-card-title class="fill-height">
              <div class="letswork-container">
                <span class="span-title">Drawings & Graphic Designs </span>
                <h1>Personal Projects</h1>
              </div>
            </v-card-title>
          </v-card>
        </v-flex>
        <v-flex xl12>
          <v-layout wrap>
            <PersonalProjects
              :key="preproject.id"
              :id="preproject.id"
              v-for="preproject in personalprojects.preproject"
              :title="preproject.title"
              :year="preproject.year"
              :thumbnail="preproject.thumbnail"
            />
          </v-layout>
        </v-flex>
      </v-layout>
      <letswork />
    </section>

    <!-- contact -->
  </v-container>
</template>

<script>
import letswork from "~/components/letswork.vue";
import PersonalProjects from "~/components/PersonalProjects.vue";
import CaseStudies from "~/components/CaseStudies.vue";
export default {
  data() {
    return {
      hover: false,
      link: true
    };
  },
  components: {
    letswork,
    CaseStudies,
    PersonalProjects
  },
  async asyncData(context) {
    const projects = await context.app.$storyapi
      .get("cdn/stories", {
        version: "draft",
        starts_with: "projects"
      })
      .then(res => {
        return {
          projects: res.data.stories.map(bp => {
            return {
              id: bp.slug,
              title: bp.content.title,
              year: bp.content.year,
              thumbnail: bp.content.thumbnail
            };
          })
        };
      });
    const personalprojects = await context.app.$storyapi
      .get("cdn/stories", {
        version: "draft",
        starts_with: "personalprojects"
      })
      .then(res => {
        return {
          preproject: res.data.stories.map(bp => {
            return {
              id: bp.slug,
              title: bp.content.title,
              year: bp.content.year,
              thumbnail: bp.content.thumbnail
            };
          })
        };
      });

    return { personalprojects, projects };
  }
};
</script>

<style lang="scss" scoped></style>
