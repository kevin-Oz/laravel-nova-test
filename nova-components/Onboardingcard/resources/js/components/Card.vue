<template>
  <VOnboardingWrapper ref="wrapper" :steps="steps" />
  <div class="btn-section">
    <button class="btn-start" @click="start()">start the tour</button>
  </div>
</template>

<script>
import { defineComponent, ref, onMounted } from 'vue';
import { VOnboardingWrapper, useVOnboarding } from 'v-onboarding';
import 'v-onboarding/dist/style.css'
export default defineComponent({

  components: {
    VOnboardingWrapper
  },

  setup() {

    let verbiage = ref([]);
    let steps = ref([]);
    const wrapper = ref(null)
    const { start, finish } = useVOnboarding(wrapper)

    onMounted(() => init());

    /**
     * This function is to get the verbiage from the server API , and add the steps to the steps array.
     * this function is called when the component is mounted.
     */
    const init = async () => {
      finish();
      verbiage = await (await Nova.request().get('/nova-vendor/onboardingcard/verbiage')).data;
      verbiage.forEach(element => {
        steps.value.push(
          {
            attachTo: { element: `#${element.id}` }, content: {
              title: element.title,
              description: element.description
            }
          }
        )
      });

      console.log(steps.value);
      setIdAttribute();
    }

    /**
     * I need to set the id attribute to the elements that I want to attach the tooltip, but i dont found a way to do it in the Nova resource,
     *  so this is not a better way to do it, but it works.
     * 
     * The better way is create a Nova template and adding the id attribute.
     * 
     */
    const setIdAttribute= ()=>{
      let element = document.querySelector("#nova > div:nth-child(2) > div.hidden.lg\\:block.lg\\:absolute.left-0.bottom-0.lg\\:top-\\[56px\\].lg\\:bottom-auto.w-60.px-3.py-8 > div > div:nth-child(2) > div > div");
      let element2 = document.querySelector("#nova > div:nth-child(2) > div.p-4.md\\:py-8.md\\:px-12.lg\\:ml-60.space-y-8 > div.relative > div.bg-white.dark\\:bg-gray-800.rounded-lg.shadow > div.relative");
      let element3 = document.querySelector("#nova > div:nth-child(2) > div.p-4.md\\:py-8.md\\:px-12.lg\\:ml-60.space-y-8 > div.relative > div.flex > div.w-full.flex.items-center.mb-6 > div > a");
      element.setAttribute("id", "step1");
      element2.setAttribute("id", "step2");
      element3.setAttribute("id", "step3");
    }

    return {
      wrapper,
      steps,
      finish,
      start

    }
  }

})


</script>

<style>
/* Scoped Styles */

.btn-start {
  padding: 5px;
  border-radius: 3.5px;
  background-color: rgba(235, 0, 59, 0.87);
  color: white;
  font-weight: bold;
}

</style>
