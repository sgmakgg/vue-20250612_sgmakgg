<script lang="ts" setup>
import type {MeetupDTO} from '@shgk/vue-course-ui'
import {UiAlert, UiContainer} from '@shgk/vue-course-ui'
import MeetupAgenda from './MeetupAgenda.vue'
import MeetupDescription from './MeetupDescription.vue'
import MeetupCover from './MeetupCover.vue'
import MeetupInfo from './MeetupInfo.vue'

defineProps<{
  meetup: MeetupDTO
}>()
</script>

<template>
  <div>
    <MeetupCover :image="meetup.image" :title="meetup.title" />
    <UiContainer>
      <div class="meetup">
        <div class="meetup__content">
          <h2>Описание</h2>
          <MeetupDescription :description="meetup.description" />
          <h2>Программа</h2>
          <MeetupAgenda v-if="meetup.agenda.length" :agenda="meetup.agenda" />
          <UiAlert v-else>Программа пока пуста...</UiAlert>
        </div>
        <div class="meetup__aside">
          <MeetupInfo :date="meetup.date" :organizer="meetup.organizer" :place="meetup.place" />
          <div class="meetup__aside-buttons"></div>
        </div>
      </div>
    </UiContainer>
  </div>
</template>

<style scoped>
.meetup {
  display: flex;
  flex-direction: column-reverse;
  gap: var(--spacing-large);
  margin-block-start: var(--spacing-large);
}

.meetup__content {
}

.meetup__aside {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-base);
}

.meetup__aside-buttons {
  padding-inline-start: calc(var(--control-size-small) + var(--spacing-small));
  display: flex;
  align-items: flex-start;
  gap: var(--spacing-smaller);
}

@media all and (min-width: 992px) {
  .meetup {
    flex-direction: row;
  }

  .meetup__content {
    flex: 1 0;
  }

  .meetup__aside {
    width: 350px;
    /* Inline with tabs */
    margin-block-start: var(--control-size);
  }

  .meetup__aside-buttons {
    flex-direction: column;
  }
}
</style>
