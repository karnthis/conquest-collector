<template>
  <v-app :style="{background: $vuetify.theme.themes.light.background}">
    <v-row class="mt-10">
      <v-col cols="12" md="4"></v-col>
      <v-col cols="12" md="4">
        <v-card>
          <v-card-title class="mb-5">
            <h1>Game Submission Form</h1>
          </v-card-title>
          <v-card-text>
            <v-form
              ref="form"
              v-model="valid"
              lazy-validation>
              <v-row class="mb-2"><h2>Player Names</h2></v-row>
              <v-row>
                <v-col>
                  <v-text-field
                    v-model="p1.name"
                    :rules="isRequired"
                    label="Player One"
                    required
                    outlined
                  ></v-text-field>
                </v-col>
                <v-col>
                  <v-text-field
                    v-model="p2.name"
                    :rules="isRequired"
                    label="Player Two"
                    required
                    outlined
                  ></v-text-field>
                </v-col>
              </v-row>

              <v-row class="mb-2"><h2>Player Factions</h2></v-row>
              <v-row>
                <v-col>
                  <v-select
                    v-model="p1.faction"
                    :items="fationItems"
                    :rules="isRequired"
                    label="Player One"
                    required
                    outlined
                  ></v-select>
                </v-col>
                <v-col>
                  <v-select
                    v-model="p2.faction"
                    :items="fationItems"
                    :rules="isRequired"
                    label="Player Two"
                    required
                    outlined
                  ></v-select>
                </v-col>
              </v-row>

              <v-row class="mb-2"><h2>Scenario Played</h2></v-row>
              <v-row>
                <v-col cols="4">
                  <v-select
                    v-model="game.type"
                    :items="typeItems"
                    :rules="isRequired"
                    label="Type"
                    required
                    outlined
                  ></v-select>
                </v-col>
                <v-col cols="8">
                  <v-text-field
                    v-model="game.id"
                    :rules="isRequired"
                    label="Name / Identifier"
                    required
                    outlined
                  ></v-text-field>
                </v-col>
                <v-col></v-col>
              </v-row>

              <v-row class="mb-2"><h2>Win / Loss / Draw / Yield</h2></v-row>
              <v-row>
                <v-col>
                  <v-select
                    v-model="p1.wldy"
                    :items="wldyItems"
                    :rules="isRequired"
                    label="Player One"
                    required
                    outlined
                  ></v-select>
                </v-col>
                <v-col>
                  <v-select
                    v-model="p2.wldy"
                    :items="wldyItems"
                    :rules="isRequired"
                    label="Player Two"
                    required
                    outlined
                  ></v-select>
                </v-col>
                <v-col></v-col>
              </v-row>

              <v-row class="mb-2"><h2>Points Played / Lost</h2></v-row>
              <v-row>
                <v-col>
                  <v-text-field
                    v-model="game.points"
                    :rules="isRequired"
                    label="Starting Points"
                    required
                    outlined
                  ></v-text-field>
                </v-col>
                <v-col>
                  <v-text-field
                    v-model="p1.lost"
                    label="P1 Points Lost"
                    outlined
                  ></v-text-field>
                </v-col>
                <v-col>
                  <v-text-field
                    v-model="p2.lost"
                    label="P2 Points Lost"
                    outlined
                  ></v-text-field>
                </v-col>
              </v-row>

              <v-row class="mb-2"><h2>Victory Points</h2></v-row>
              <v-row>
                <v-col>
                  <v-text-field
                    v-model="p1.vp"
                    :rules="isRequired"
                    label="Player One"
                    required
                    outlined
                  ></v-text-field>
                </v-col>
                <v-col>
                  <v-text-field
                    v-model="p2.vp"
                    :rules="isRequired"
                    label="Player Two"
                    required
                    outlined
                  ></v-text-field>
                </v-col>
                <v-col>
                  <v-text-field
                    v-model="game.vp"
                    :rules="isRequired"
                    label="Required"
                    required
                    outlined
                  ></v-text-field>
                </v-col>
              </v-row>

              <v-row class="mb-2"><h2>Rounds</h2></v-row>
              <v-row>
                <v-col>
                  <v-text-field
                    v-model="game.end"
                    :rules="isRequired"
                    label="Round Finished"
                    required
                    outlined
                  ></v-text-field>
                </v-col>
                <v-col>
                  <v-text-field
                    v-model="game.max"
                    :rules="isRequired"
                    label="Round Limit"
                    required
                    outlined
                  ></v-text-field>
                </v-col>
                <v-col></v-col>
              </v-row>

            </v-form>
          </v-card-text>

          <v-card-actions>
            <v-row>
              <v-spacer></v-spacer>
              <v-btn @click="submitForm" class="ma-5" color="green">SUBMIT</v-btn>
            </v-row>
          </v-card-actions>
        </v-card>
      </v-col>
      <v-col cols="12" md="4"></v-col>
    </v-row>
  </v-app>
</template>

<script>
// import SingleFormField from '@/components/SingleFormField'

export default {
  name: 'App',

  components: {},
  methods: {
    submitForm () {
      if (this.$refs.form.validate()) {
        fetch('https://api.squirrellogic.com', {
          method: 'POST',
          mode: 'cors',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            p1: this.p1,
            p2: this.p2,
            game: this.game
          })
        })
          .then(res => res.json())
          .then(res => {
            console.dir(res)
            alert('Thank you for your submission')
          })
      } else {
        alert('Please complete required fields')
      }
    }
  },
  data: () => ({
    valid: false,
    p1: {},
    p2: {},
    game: {},
    isRequired: [
      v => !!v || 'Field is Required'
    ],
    fationItems: [
      '100K',
      'Spires',
      'Dweghom',
      'Nords',
      'W\'Hadrun'
    ],
    wldyItems: [
      'Win',
      'Loss',
      'Draw',
      'Yield'
    ],
    typeItems: [
      'Official',
      'Beta',
      'Custom'
    ]
  })
}
</script>

<style>
html, body {
  background-color: gray;
}
</style>
