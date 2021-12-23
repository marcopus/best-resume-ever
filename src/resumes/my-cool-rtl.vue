<template>
  <div class="resume">
    <div class="banner">
      <div class="banner__fullname">{{ person.name.first }} {{ person.name.middle }} {{ person.name.last }}</div>
      <div class="banner__position">{{ person.position }}</div>
      <div class="banner__location">{{ lang.born }} {{person.birth.date}} {{ lang.bornIn }} {{person.birth.location}}</div>
      <div class="banner__location">{{ lang.nationality }} {{person.birth.nationality}}</div>
    </div>

    <div class="content">
      <div class="content__right">
        <div class="section">
          <div class="section-headline">
            <i class="section-headline__icon material-icons">work</i>{{ lang.experience }}
          </div>

          <div class="section-content">
            <div
              v-for="(experience, index) in person.experience"
              class="section-content__item">

              <a 
                class="section-content__header"
                :key="index"
                :class="{ link: experience.website !== undefined}"
                :href="experience.website">
                {{ experience.position }}
              </a>
              <span class="section-content__subheader">
                {{ experience.company }}
                <span class="section-content__plain">{{ experience.location }}</span>
              </span>

              <div class="section-content__text">{{ experience.timeperiod }}</div>
              <span class="section-content__text--light">{{ experience.description }}</span>
            </div>
          </div>
        </div>

        <div class="section">
          <div class="section-headline">
            <i class="section-headline__icon material-icons">school</i>{{ lang.education }}
          </div>

          <div class="section-content">
            <div
              v-for="(education, index) in person.education"
              class="section-content__item">

              <span class="section-content__header"> {{ education.school }} </span>
              <span class="section-content__plain">{{ education.location }}</span>
              <span class="section-content__subheader">{{ education.degree }}</span>
              <span class="section-content__text"> {{ education.timeperiod }} </span>
              <a
                class="section-content__text--light"
                :key="index"
                :class="{ link: education.website !== undefined}"
                :href="education.website">
                {{ education.description }}
              </a>
            </div>
          </div>
        </div>

        <div
          v-if="person.projects"
          class="section">
          <div class="section-headline">
            <i class="section-headline__icon material-icons">code</i>{{ lang.projects }}
          </div>

          <div class="section-content-grid__left">
            <div v-for="(project, index) in person.projects" :key="index"
              class="section-content__item-grid">
              <a
                class="section-content__header"
                :class="{ link: project.url !== undefined}"
                :href="project.url">
                {{ project.name }}
              </a>
              <span class="section-content__subheader">{{ project.platform }}</span>
              <span class="section-content__text"> {{ project.description }} </span>
            </div>
          </div>
        </div>

        <div
          v-if="person.contributions"
          class="section">
          <div class="section-headline">
            <i class="section-headline__icon fa fa-heart"></i>{{lang.contributions}}
          </div>

          <div class="section-content-grid__left">
            <a
              v-for="(contribution, index) in person.contributions"
              class="section-content__item-grid"
              :key="index"
              :class="{ link: contribution.url !== undefined}"
              :href="contribution.url">
              <span class="section-content__header"> {{ contribution.name }} </span>
              <span class="section-content__text"> {{ contribution.description }} </span>
              <span class="section-content__text--light" style="word-break: break-all;">
                {{ contribution.url }}
              </span>
            </a>
          </div>
        </div>
      </div>
      <div class="content__left">
        <div class="section">
          <div class="section-headline">{{ lang.about }}</div>

          <div class="section-content section-content--plain">
            {{ person.about }}
            <br/><em>{{ person.about2 }}</em>
          </div>
        </div>

        <div
          v-if="person.skills"
          class="section">
          <div class="section-headline">
            {{ lang.skills }}
          </div>

          <div class="section-content-grid">
            <a
              v-for="(skill, index) in person.skills"
              class="grid-item"
              :key="index"
              :class="{ link: skill.url !== undefined}"
              :href="skill.url">
              <span class="squarred-grid-item">
                {{ skill.name }}
              </span>
            </a>
          </div>
          <div class="section-content section-content--plain">
            <br/>
            {{ person.knowledge }}
          </div>
          <div class="section-content section-content--plain">
            {{ lang.languages }}: {{ person.languages }}
          </div>
        </div>

        <div class="section">
          <div class="section-headline">
            {{ lang.contact }}
          </div>

          <div class="section-content section-content--plain">
            <div class="section-link">
              <i class="section-link__icon material-icons">home</i>{{ person.contact.street }}<br/>{{ person.contact.city }}
            </div>

            <div class="section-link">
              <i class="section-link__icon material-icons">mail</i>
              <a
                class="link"
                :href="contactLinks.email">
                {{ person.contact.email }}
              </a>
            </div>

            <div class="section-link">
              <i class="section-link__icon material-icons">phone</i>{{ person.contact.phone }}
            </div>

            <div 
              v-if="person.contact.website"
              class="section-link">
              <i class="section-link__icon fa fa-globe"></i>
              <a
                class="link"
                :href="'https://'+person.contact.website">
                {{ person.contact.website }}
              </a>
            </div>

            <div
              v-if="person.contact.linkedin"
              class="section-link">
              <i class="section-link__icon fa fa-linkedin"></i>
              <a
                class="link"
                :href="contactLinks.linkedin">
                {{ person.contact.linkedin }}
              </a>
            </div>

            <div
              v-if="person.contact.github"
              class="section-link">
              <i class="section-link__icon fa fa-github"></i>
              <a
                class="link"
                :href="contactLinks.github">
                {{ person.contact.github }}
              </a>
            </div>

            <div
              v-if="person.contact.gitlab"
              class="section-link">
              <i class="section-link__icon fa fa-gitlab"></i>
              <a
                class="link"
                :href="'https://gitlab.com/'+person.contact.gitlab">
                {{ person.contact.gitlab }}
              </a>
            </div>

            <div
              v-if="person.contact.medium"
              class="section-link">
              <i class="section-link__icon fa fa-medium"></i>
              <a
                class="link"
                :href="contactLinks.medium">
                {{ person.contact.medium }}
              </a>
            </div>
            
          </div>
        </div>
        
        <div class="section">
          <div class="section-headline">
            {{ lang.interests }}
          </div>
          <div class="interests-content">
            <a v-for="(interest, index) in person.interests" :key="index"
              class="interest-item"
              :href="interest.url">

              <i v-if="interest.iconClass" :class="interest.iconClass + ' interest-item__icon'"></i>
              <span class="interest-item__icon-label"> {{ interest.name }} </span>
            </a>
          </div>
        </div>
      </div>
    </div>

    <img class="picture"/>
  </div>
</template>

<script>
import Vue from 'vue';
import { getVueOptions } from './options';

const name = 'my-cool-rtl';

export default Vue.component(name, getVueOptions(name));
</script>

<style lang="less" scoped>
@accent-color: #34495E;
@banner-color: #42b883;
@banner-height: 120px;
@picture-size: 120px;
@picture-offset: 35px;
@base-padding: 30px;
@left-column-width: 240px;

.link {
  color: inherit;
  cursor: pointer;
  text-decoration-line: underline;

  &:visited {
    color: inherit;
  }
}

.resume {
  position: relative;
  font-family:'Roboto' !important;
  font-size: 0.9em;
}

.picture {
  position: absolute;
  top: @banner-height - @picture-offset;
  left: @left-column-width + @base-padding * 2 - @picture-size / 2;
  height: @picture-size;
  width: @picture-size;
  border-radius: 50%;
  border: 5px solid @accent-color;
  content: url('../../resume/id.jpg');
  z-index: 2;
}

.banner {
  width: calc(100% - @base-padding * 2);
  height: @banner-height;
  padding: @base-padding;
  background-color: @banner-color;

  color: white;

  &__fullname {
    font-size: 32px;
  }

  &__position {
    font-size: 16px;
  }

  &__location {
    font-size: 12px;
  }
}

.content {
  display: flex;
  width: 100%;
  height: 100%;

  &__left,
  &__right {
    height: 100%;
    padding: @base-padding;
  }

  &__left {
    width: @left-column-width;
    color: rgba(255, 255, 255, 0.59);
    background-color: @accent-color;

    .section-headline {
      color: white;
    }
  }

  &__right {
    flex: 1;
  }
}

.section {
  margin: 20px 0;
}

.section-link,
.section-headline {
  display: flex !important;
  align-items: center;
  color: @accent-color;
  display: inline-block;
  font-size: 1.2em;
  margin: 8px 0;

  &__icon {
    margin-right: 8px;
    font-size: 1.4em;
  }
}

.section-link {
  font-size: 1.1em;
  color: rgba(255, 255, 255, 0.59) !important;

  &__icon {
    color: white;
  }
}

.section-content {
  margin-top: 5px;
  padding-left: 32px;
  font-size: 14px;

  &__item {
    display: block;
    margin-bottom: 5px;
  }

  &__header {
    display: block;
    font-size: 1.1em;
    font-weight: 500;
  }

  &__subheader {
    display: block;
    font-weight: 400;
  }

  &__plain,
  &__text {
    display: block;
    font-size: 12px;

    &--light {
      font-size: 12px;
    }
  }

  &__plain {
    display: inline;
    font-weight: 300;
  }

  &__item-grid {
    flex: 1 1 0;
    margin-bottom: 5px;
    padding-right: 5px;
  }

  &--plain {
    padding: 0;
  }
}

.section-content-grid {
  display: flex;
  flex-wrap: wrap;
  margin-top: 5px;
  margin-bottom: 5px;
  
  &__left {
    padding-left: 32px;
  }
}

.grid-item {
  padding-right: 5px;
}

.squarred-grid-item {
  display: block;
  border: 1px solid white;
  color: white;
  margin-top: 5px;
  padding: 5px;
}

.interests-content {
  display: flex;
  flex-direction: column;
}

.interest-item {
  display: grid;
  grid-template-columns: 30px auto;

  color: rgba(255, 255, 255, .6);

  margin-right: 25px;
  margin-bottom: 10px;

  transition: .5s;

  &:hover {
    color: rgba(255, 255, 255, .8);
    transition: .5s;
  }
}

.interest-item__icon {
  font-size: 1.3em;
}

.interest-item__icon-label {
  top: 2.5px;
  position: relative;
}

.subheadline {
  color: rgba(255, 255, 255, .8);
  font-size: 1.2em;

  display: block;
  margin-bottom: 10px;
}

</style>
