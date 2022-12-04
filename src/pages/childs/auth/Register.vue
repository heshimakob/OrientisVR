<template>
  <div class="flex flex-center">
    <div>
      <div class="q-mb-lg q-mt-lg">
        <img src="others/21.jpg" style="max-width: 150px" />
      </div>
      <h1 class="AFJfont--bold AFJfs--24 default-title">
        Rejoignez <span class="text-primary">Orientis</span>
      </h1>
      <div>
        <q-form
          @submit="onSubmit"
          @reset="onReset"
          class="q-gutter-"
          style="width: 300px"
        >
          <div class="AFJinput text-left">
            <span class="label">Indentifiant</span>
            <q-input
              filled
              v-model="title"
              placeholder="Identifiant *"
              hint="Nom ou Adresse mail"
              lazy-rules
              :rules="[
                (val) => (val && val.length > 0) || 'Ooups Champs recqui, Identifiant',
              ]"
            />
          </div>

          <div class="AFJinput text-left q-mt-lg">
            <span class="label">Mot de passe</span>
            <q-input
              filled
              type="password"
              v-model="password"
              placeholder="Mot de passe *"
              hint="Mot de passe"
              lazy-rules
              :rules="[
                (val) =>
                  (val !== null && val !== '') || 'Ooups Champs recqui, Mot de passe',
                (val) => (val && val.length > 2) || 'Mot de passe court',
              ]"
            />
          </div>

          <div class="q-mt-lg">
            <q-btn
              label="S'inscrire"
              type="submit"
              color="primary"
              class="q-mt-sm full-width AFJbtn"
            />
          </div>
        </q-form>
        <div class="q-mt-md q-mL-md tex-center flex row justify-between">
          <q-item class="caption tex-center">
            <span class="AFJcolor--g AFJfs--12">© 2022 Orientis, Inc.</span>
          </q-item>
          <q-btn
            class="AFJbtn--small"
            icon="eva-github"
            text-color="primary"
            label="Sources"
            target="_blank"
            type="a"
            href="https://github.com/heshimakob/orientis"
          ></q-btn>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { useQuasar } from "quasar";
import { defineComponent, ref, onMounted } from "vue";
import userData from "local-storage";
import { api } from "boot/axios";

export default defineComponent({
  name: "Register",
  component: {},
  setup: () => {
    const $q = useQuasar();

    let title = ref(null);
    let password = ref(null);
    function notifErrReg() {
      $q.notify({
        message: "Impossible de créer le compte",
        type: "negative",
        progress: true,
        timeout: 5000,
      });
    }
    function notifSucReg() {
      $q.notify({
        message: "Impossible de créer le compte",
        type: "negative",
        progress: true,
        timeout: 5000,
      });
    }

    function notifErrServe() {
      $q.notify({
        message: "Erreur Fatale ! Connexion serveur échouée",
        type: "warning",
        progress: true,
        timeout: 10000,
      });
    }

    onMounted(() => {
      function onReset() {}
      onReset();
    });

    return {
      // Méthodes
      // Objets
      title,
      password,
      accept: ref(false),
    };
  },
});
</script>
