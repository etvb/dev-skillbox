<template>
  <div id="navbar-web2">
    <div>
      <nav class="navbar2" role="navigation" aria-label="main navigation">
        <div class="navbar-brand">
          <!-- nuxt-imagen -->
          <!-- start button hamburger -->
          <div
            @click="openMenu2"
            role="button"
            class="navbar-burger burger"
            aria-label="menu"
            aria-expanded="false"
            data-target2="navbar2"
          >
            <span aria-hidden="true" />
            <span aria-hidden="true" />
            <span aria-hidden="true" />
          </div>
          <!-- end button hamburger -->
        </div>
        <div id="navbar2" class="navbar-menu">
          <!-- aqui poner los botones -->


          <nav id="search">
            <!-- {{ $route.query.price }} -->
            <!--start buttom language -->
            <div class="button-search">
              <i class="fas fa-globe" />
              <span class="titleButtom">Language</span>
              <!-- {{ search }} -->
              <b-field>
                <!-- :input="searchInstructors()" -->
                <b-select
                  v-model="search"  
          
                  placeholder="Select language"
                  size="is-small"
                >
                  <option
                    v-for="language in languages"
                    :value="language.id"
                    :key="language.id"
                  >
                    {{ language.english }}
                  </option>
                  <option value="others">
                    Other languages
                  </option>
                </b-select>
              </b-field>
            </div>
        
            <!-- button-Availability -->
            <div @click="showMe()" class="button-search">
              <i class="far fa-calendar-alt" />

              <span class="titleButtom">Availability</span>
              <br>
              <div>
                {{ daysChecked }}
                <span class="sizeSmall">Su</span>
                <span class="sizeSmall">Mo</span>
                <span class="sizeSmall">Tu</span>
                <span class="sizeSmall">We</span>
                <span class="sizeSmall">Th</span>
                <span class="sizeSmall">Fr</span>
                <span class="sizeSmall">Sa</span>
                <i class="fas fa-angle-down" />
              </div>
              <div id="menu" class="days">
                <div
                  v-for="day in days"
                  :key="day.id"
                  class="field"
                >
                  <b-checkbox
                    v-model="daysChecked"
                    :native-value="day.id"
                    :input="searchInstructors()"
                  >
                    {{ day.name }}
                  </b-checkbox>
                </div>
              </div>
            </div>
            <!-- end button-Availability -->

            <!-- button-Speaker -->
            <div class="button-search">
              <i class="fas fa-chalkboard-teacher" />
              <span class="titleButtom">Native Speaker</span>

              <b-field>
                <b-select
                  size="is-small"
                  expanded="true"                     
                >
                  <option value="0">
                    YES
                  </option>
                  <option value="1">
                    NO
                  </option>
                </b-select>
              </b-field>
            </div>
            <!--end button-Speaker -->

            <!-- Lesson Price -->
            <div class="button-search">
              <i class="far fa-money-bill-alt" />
              <span class="titleButtom">Lesson Price</span>
              <div>
                <!-- <i class="fas fa-angle-down" /> -->
                <div class="contentNumber">
                  <input
                    v-model="range[0]"
                    :max="range[1]"
                    class="sizeNumber"
                    type="number"
                    placeholder="Min 0"
                    min="0"
                  >
                  <input
                    v-model="range[1]"
                    :min="range[0]"
                    class="sizeNumber"
                    type="number"
                    placeholder="Max 50"
                    max="50"
                  >
                </div>
              </div>
            </div>
            <!--end Lesson Price -->

            <!-- localtion -->
            <div class="button-search">
              <i class="fas fa-chalkboard-teacher" />
              <span class="titleButtom">Location</span>

              <b-field>
                <b-select                         
                  placeholder=""
                  size="is-small"
                >
                  <option value="0">
                    Mexíco
                  </option>
                  <option value="1">
                    Alemani alemania
                  </option>
                </b-select>
              </b-field>
            </div>
            <!--end localtion -->

            <!-- rating -->
            <div class="button-search">
              <i class="fas fa-chalkboard-teacher" />
              <span class="titleButtom">Rating</span>

              <b-field>
                <b-select  
                  expanded="true"                     
                  placeholder=""
                  size="is-small"
                  class="prueba"
                >
                  <option value="0">
                    *
                  </option>
                  <option value="2">
                    * *
                  </option>
                  <option value="3">
                    * * *
                  </option>
                  <option value="4">
                    * * * *
                  </option>
                </b-select>
              </b-field>
            </div>
            <!--end rating -->
          </nav>
        </div>
      </nav>
    </div>
  </div>
</template>
<script>
export default {
  methods: {
    openMenu2(event) {
      const element = event.target
      const trigger = element.closest('div')

      const target = trigger.dataset.target2
      const $target = document.getElementById(target)

      trigger.classList.toggle('is-active')
      $target.classList.toggle('is-active')
    }
  }
}
</script>
