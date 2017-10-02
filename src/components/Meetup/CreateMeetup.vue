<template>
  <v-container>
    <v-layout row>
      <v-flex xs12 sm6 offset-sm3>
        <h4>Create a new Meetup</h4>
      </v-flex>
    </v-layout>
    <v-layout row>
      <v-flex xs12>
        <form @submit.prevent="onCreatedMeetup">
          <v-layout row>
            <v-flex xs12 sm6 offset-sm3>
              <v-text-field name="title" label="Title" id="title" v-model.trim="meetup.title" required></v-text-field>
            </v-flex>
          </v-layout>
          <v-layout row>
            <v-flex xs12 sm6 offset-sm3>
              <v-text-field name="location" label="Location" id="location" v-model.trim="meetup.location" required></v-text-field>
            </v-flex>
          </v-layout>
          <v-layout row>
            <v-flex xs12 sm6 offset-sm3>
              <v-text-field name="imgUrl" label="Image URL" id="imgUrl" v-model.trim="meetup.imgUrl" required></v-text-field>
            </v-flex>
          </v-layout>
          <v-layout row>
            <v-flex xs12 sm6 offset-sm3>
              <img :src="meetup.imgUrl" height="150">
            </v-flex>
          </v-layout>
          <v-layout row>
            <v-flex xs12 sm6 offset-sm3>
              <v-text-field name="description" label="Description" id="description" multi-line v-model.trim="meetup.description" required></v-text-field>
            </v-flex>
          </v-layout>
          <v-layout row >
            <v-flex xs12 offset-sm3>
              <v-date-picker v-model="meetup.date"></v-date-picker>
              {{meetup.date}}
            </v-flex>
            <v-flex xs12 offset-sm3>
              <v-time-picker v-model="meetup.time"></v-time-picker>
              {{meetup.time}}
            </v-flex>
          </v-layout>
          <v-layout>
            <v-flex xs12 sm6 offset-sm3>
              <v-btn class="primary"  type="submit" :disabled="!formIsValid">Create Meetup</v-btn>
            </v-flex>
          </v-layout>
        </form>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  name: 'CreateMeetup',
  data () {
    return {
      meetup: {
        title: '',
        location: '',
        imgUrl: '',
        description: '',
        date: new Date(),
        time: new Date()
      }
    }
  },
  computed: {
    formIsValid: function () {
      console.log(this.meetup)
      return this.meetup.title !== '' &&
        this.meetup.location !== '' &&
        this.meetup.imgUrl !== '' &&
        this.meetup.description !== ''
    }
  },
  methods: {
    onCreatedMeetup () {
      if (!this.formIsValid) {
        return
      }
      this.$store.dispatch('createMeetup', this.meetup)
      this.$router.push('/meetups')
    }
  }
}
</script>