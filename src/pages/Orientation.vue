<template>
  <q-page class="AFJpage">
    <div class="AFJpage__header row justify-center flex flex-center relative-position">
      <div class="text-center">
        <h1 class="AFJfont--bold AFJfs--28">Orientation</h1>
        <div class="q-mb-lg q-pt-xs">
          <p class="AFJcolor--g">
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Doloribus at sint
            reiciendis magni, pariatur a ullam unde odio assumenda sit tempore voluptatum
          </p>
        </div>
        <div class="row justify-center">
          <q-tabs v-model="tab" dense class="AFJtab--simple AFJtab--simple q-gutter-lg">
            <q-tab name="infos" label="Questionnaire" />
            <q-tab name="notifs" label="Domaine Aptes" />
            <q-tab name="cat" label="Resultat" />
          </q-tabs>
        </div>
      </div>

      <div class="AFJpage__header__img">
        <div class="l">
          <img src="banners/png/4.png" alt="" />
        </div>
        <div class="r">
          <img src="banners/png/pablita-631.png" alt="" />
        </div>
      </div>
    </div>

    <div class="AFJcontainer AFJcontainer__fxs overflow-hidden">
      <div class="row justify-lg-start no-wrap">
        <div class="full-width">
          <h2 class="AFJfont--bold AFJfs--20 no-wrap row justify-between">
            <div>
              <q-icon
                name="eva-award-outline"
                class="AFJcolor--g q-mr-md"
                style="margin-top: -3px"
              />
              Quelques renseignement sur vos preference
              <span class="AFJfont--medium AFJfs--14 AFJcolor--g q-ml-md">
                <span> (questions </span>
                <span> ) </span>
              </span>
            </div>
            <div style="margin-right: 1.5rem !important">
              <q-btn
                @click="parseInt(accountType) > 2 ? upMyInfo(univ) : upAdminInfo()"
                color="white"
                icon="eva-done-all-outline"
                text-color="primary"
                class="AFJcolor--white AFJbtn full-width"
                label="Confirmer"
              />
            </div>
          </h2>

          <div class="AFJbox q-mr-lg">
            <q-form @submit="onSubmit" @reset="onReset" class="q-gutter-md">
              <div class="row justify-between AFJfield--container-half">
                <div class="AFJinput">
                  <div>
                    <span class="label">1. Quelle est ta façon de penser?</span>
                  </div>
                  <div class="q-pa-md">
                    <div class="q-gutter-sm">
                      <q-radio v-model="shape" val="line" label="Line" />
                      <q-radio v-model="shape" val="rectangle" label="Rectangle" />
                      <q-radio v-model="shape" val="ellipse" label="Ellipse" />
                      <q-radio v-model="shape" val="polygon" label="Polygon" />
                    </div>
                  </div>
                  creative rapide logique
                </div>
                <div class="AFJinput">
                  <span class="label">2. Quelle type de personne est tu?</span>

                  introverti extraverti unpeu le deux


                </div>
              </div>
              <div class="row justify-between AFJfield--container-half">
                <div class="AFJinput">
                  <div>
                    <span class="label">3. Quel problème resoudrais-tu en premier?</span>
                  </div>

                  <div class="flex justify-between q-mt-lg">
                    <q-checkbox
                      style="margin-left: -10px"
                      label="A. Economie"
                    />
                    <q-checkbox
                      style="margin-left: -10px"
                      label="B. Santé"
                    />
                    <q-checkbox
                      style="margin-left: -10px"
                      label="C. Education"
                    />
                  </div>
                </div>
                <div class="AFJinput">
                  <span class="label">4. Choisie une de ces propositions?</span>
                  <div class="flex justify-between q-mt-lg">
                    <q-checkbox
                      style="margin-left: -10px"
                      label="A. Agilté"
                    />
                    <q-checkbox
                      style="margin-left: -10px"
                      label="B. Force"
                    />
                    <q-checkbox
                      style="margin-left: -10px"
                      label="C. Dexetérité"
                    />
                  </div>
                </div>
                <div class="AFJinput">
                  <div>
                    <span class="label">5. A qui te joindrais-tu lors d'un evenement social?</span>
                  </div>

                  <div class="flex justify-between q-mt-lg">
                    <q-checkbox
                      style="margin-left: -10px"
                      label="A. Petit groupe ayant une discusion animée"
                    />
                    <q-checkbox
                      style="margin-left: -10px"
                      label="B. Grand groupe qui rit beaucoup"
                    />
                    <q-checkbox
                      style="margin-left: -10px"
                      label="C. Groupe de plusieurs personnes jouant à un jeu"
                    />
                  </div>
                </div>

                <div class="AFJinput">
                  <span class="label">6. La quelle de ces activités aimes-tu le plus faire?</span>
                  <div class="flex justify-between q-mt-lg">
                    <q-checkbox
                      style="margin-left: -10px"
                      label="A. Agilté"
                    />
                    <q-checkbox
                      style="margin-left: -10px"
                      label="B. Force"
                    />
                    <q-checkbox
                      style="margin-left: -10px"
                      label="C. Dexetérité"
                    />
                  </div>
                </div>
              </div>
            </q-form>
          </div>
        </div>

      </div>
    </div>

  </q-page>
</template>

<script>
import { defineComponent, ref, reactive } from "vue";
import userData from "local-storage";
import { useRouter, useRoute } from "vue-router";
import { api } from "boot/axios";

const univOptionsString = reactive([
  "UCB - Université Catholique de Bukavu",
  "UEA - Université Evangelique en Afrique",
  "UOB - Université Officiel de Bukavu",
]);

export default defineComponent({
  name: "Orientation",
  setup: () => {
    const router = useRouter();
    const sessionExists = () => {
      return userData.get(2000);
      shape: ref('line')

    };
    if (!sessionExists()) {
      router.push("/auth");
    }
    //Variables
    var userName = "";

    return {
      tab: ref("infos"),
      appLink: "https://Orientis.vercel.app",
      userName,

      //Select functions

      createVakueUniv(val, done) {
        if (val.length > 0) {
          if (!univOptionsString.includes(val)) {
            univOptionsString.push(val);
          }
          done(val, "toggle");
        }
      },
      filterUniv(val, update) {
        setTimeout(() => {
          update(() => {
            if (val === "") {
              univOptions.value = univOptionsString;
            } else {
              const needle = val.toLowerCase();
              univOptions.value = univOptionsString.filter(
                (v) => v.toLowerCase().indexOf(needle) > -1
              );
            }
          });
        }, 500);
      },
      createValuefavCats(val, done) {
        if (val.length > 0) {
          if (!favCatsOptionsString.includes(val)) {
            favCatsOptionsString.push(val);
          }
          done(val, "toggle");
        }
      },

      filterfavCats(val, update) {
        setTimeout(() => {
          update(() => {
            if (val === "") {
              favCatsOptions.value = favCatsOptionsString;
            } else {
              const needle = val.toLowerCase();
              favCatsOptions.value = favCatsOptionsString.filter(
                (v) => v.toLowerCase().indexOf(needle) > -1
              );
            }
          });
        }, 500);
      },
    };
  },
});
</script>
