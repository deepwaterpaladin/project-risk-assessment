<template>
  <div id="dropDown" v-if="displayDropDown == true">
    <label> {{ $t("navigateSectionLabel") }} </label>
    <div>
      <b-col md="4">
        <!-- Calls redirectToPage function whenever user changes index -->
        <select class="dropDownList" @change="redirectToPage()">
          <option select>{{ $t("selectSection") }} </option>
          <option v-for="page in totalPages" :key="page.num">
            {{ "Section " + page.num + ": " + page.title }}
          </option>
        </select>
      </b-col>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import { Model } from "survey-vue";
import i18n from "@/plugins/i18n";

@Component
export default class DropDown extends Vue {
  @Prop() public survey?: Model;
  @Prop() displayDropDown?: boolean;

  redirectToPage() {
    //colon value used to determine weather to set new value as single digit number or double digit
    var colon = ":";
    var e = document.getElementsByClassName(
      "dropDownList"
    )[0] as HTMLSelectElement;
    //Used to get selected item
    var pageSection = e.options[e.selectedIndex].text;
    var newVal: any;
    //Using regex (regular expressions)
    newVal = pageSection.replace(/\D/g, "");
    //To redirect to correct page
    if (this.survey != null) {
      this.survey.currentPageNo = newVal - 1;
    }
  }
  data() {
    return {
      totalPages: [
        {
          title: this.$t("projectDetails"),
          num: 1
        },
        {
          title: this.$t("riskAssessment"),
          num: 2
        },
        {
          title: this.$t("personalInformation"),
          num: 3
        },
        {
          title: this.$t("duelUse"),
          num: 4
        },
        {
          title: this.$t("mitigationEfforts"),
          num: 5
        }
      ]
    };
  }
}
</script>
