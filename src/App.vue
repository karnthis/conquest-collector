<template>
  <v-app>
    <v-row class="mt-10">
      <v-col cols="12" md="4"></v-col>
      <v-col cols="12" md="4">
        <v-card>
          <v-card-title>
            <h1>Game Submission Form</h1>
          </v-card-title>
          <v-card-text>

            <v-row><h2>Player Names</h2></v-row>
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

            <v-row><h2>Win / Loss / Draw / Yield</h2></v-row>
            <v-row>
              <v-col>
                <v-text-field
                  v-model="p1.wldy"
                  :rules="isRequired"
                  label="Player One"
                  required
                  outlined
                ></v-text-field>
              </v-col>
              <v-col>
                <v-text-field
                  v-model="p2.wldy"
                  :rules="isRequired"
                  label="Player Two"
                  required
                  outlined
                ></v-text-field>
              </v-col>
              <v-col></v-col>
            </v-row>

            <v-row><h2>Points Played / Lost</h2></v-row>
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

            <v-row><h2>Victory Points</h2></v-row>
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

            <v-row><h2>Rounds</h2></v-row>
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

          </v-card-text>
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

  data: () => ({
    p1: {},
    p2: {},
    game: {},
    isRequired: [
      v => !!v || 'Field is Required'
    ]
  })
}
</script>
