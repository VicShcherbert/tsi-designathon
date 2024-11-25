<template>
  <h1 style="text-align: center; margin-top: 20px">Trans-Systems Directory</h1>
  <v-container>
    <v-row>
      <v-col v-for="(person) in payload" :key="person.id" cols="12" lg="4" variant="elevated">
        <v-card color="surface-variant" style="min-height: 250px; border-radius: 10px; display: flex;">
          <v-row>
            <v-col cols="5" style="display: grid; place-content: center; padding-left: 30px;">
              <v-img width="125px" height="125px" :src="imageURL(person.thumbnailURI)" style="padding-left: 100px; border-radius: 10px;"/>
            </v-col>
            <v-col cols="7" style="display: grid; place-content: center; text-align: center;">
              <v-card-item>
                <v-card-title>
                  {{ person.firstName }} {{ person.lastName }}
                </v-card-title>
              </v-card-item>
              <v-card-text>
                <b>Department:</b> <br/>
                {{ person.jobTitle }}, {{ department(person.department) }} <br/>
                <b>Phone Number:</b> <br/>
                {{ person.phone }} <br />
                <b>Email: </b><br/>
                {{ person.email }}<br />
              </v-card-text>
            </v-col>
          </v-row>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup lang="ts">
const payload = usePayload()

//Helper functions. Some people don't have an image or a department.
const imageURL = (url: string|null) => {
  if (url === null) {
    return "https://cdn-icons-png.freepik.com/512/1077/1077114.png"
    // Some people don't have an image. I found a placeholder image online and I use that for those people.
  } else {
    return url
  }
}

const department = (name: string|null) => {
  if (name === null){
    return "No Department"
  } else {
    return name
  }
}
</script>