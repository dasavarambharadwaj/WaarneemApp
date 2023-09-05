<template>
  <div class="flex flex-col w-full gap-2 justify-between h-full">
    <div class="flex grow flex-col gap-2 justify-start">
      <Form :model="formModel" label-position="top">
        <FormItem label="Title">
          <Input
            size="large"
            v-model="formModel.title"
            placeholder="please enter title"
          />
        </FormItem>
        <FormItem label="Description">
          <Input
            size="large"
            type="textarea"
            v-model="formModel.description"
            placeholder="please enter description"
          />
        </FormItem>
        <FormItem label="Dates" class="w-full form-item-full-width">
          <template v-slot:label>
            <div class="flex justify-between items-center">
              <span>Dates</span>
              <Button
                size="large"
                icon="md-add"
                type="primary"
                shape="circle"
                @click="addDate"
              ></Button>
            </div>
          </template>
          <date-picker v-model="selectedDate.date" is-inline>
            <template #default="{ inputValue, togglePopover, hidePopover }">
              <div class="flex flex-wrap">
                <button
                  v-for="(date, i) in formModel.dates"
                  :key="date.date.getTime()"
                  class="flex items-center bg-indigo-100 hover:bg-indigo-200 text-sm text-indigo-600 font-semibold h-8 px-2 m-1 rounded-lg border-2 border-transparent focus:border-indigo-600 focus:outline-none"
                  @click.stop="dateSelected($event, date, togglePopover)"
                  ref="button"
                >
                  {{ date.date.toLocaleDateString() }}
                  <Button
                    icon="md-close"
                    shape="circle"
                    @click.stop="removeDate(date, hidePopover)"
                  ></Button>
                </button>
              </div>
            </template>
          </date-picker>
        </FormItem>
      </Form>
      <div class="gap-2 flex flex-col overflow-auto justify-start">
        <Card v-for="dateForm in formModel.dates" :key="dateForm.uid">
          <div class="flex">
            <Form
              :model="dateForm"
              label-position="top"
              class="flex flex-wrap gap-2"
            >
              <FormItem label="Start Time" class="w-[48%]">
                <TimePicker
                  transfer
                  class="w-full"
                  v-model="dateForm.details.startTime"
                ></TimePicker>
              </FormItem>
              <FormItem label="End Time" class="w-[48%]">
                <TimePicker
                  transfer
                  class="w-full"
                  v-model="dateForm.details.endTime"
                ></TimePicker>
              </FormItem>
              <FormItem label="Price" class="w-[48%]">
                <InputNumber
                  class="w-full"
                  v-model="dateForm.details.price"
                ></InputNumber>
              </FormItem>
              <FormItem label="Type" class="w-[48%]">
                <Select class="w-full" v-model="dateForm.details.type" transfer>
                  <Option
                    v-for="item in types"
                    :key="item"
                    :label="item"
                    :value="item"
                  ></Option>
                </Select>
              </FormItem>
            </Form>
            <Button
              type="warning"
              icon="md-trash"
              class="shrink-0"
              shape="circle"
              @click.stop="removeDate(dateForm)"
            ></Button>
          </div>
        </Card>
      </div>
    </div>
    <div class="flex gap-2 w-full">
      <Button size="large" @click="deleteItem" class="w-1/2">Delete</Button>
      <Button size="large" type="primary" class="w-1/2" @click="save"
        >Save</Button
      >
    </div>
  </div>
</template>
<script>
import DatePicker from "v-calendar/lib/components/date-picker.umd";
export default {
  emits: ["input", "delete-shift"],
  components: { DatePicker },
  props: {
    value: {
      type: Object,
      default() {
        return {};
      },
    },
  },
  data() {
    return {
      formModel: {},
      selectedDate: {},
      types: ["Consultation", "Telephone", "Ambulance"],
    };
  },
  created() {
    this.formModel =
      Object.keys(this.value) > 0 ? this.value : this.getDefaultForm();
  },
  methods: {
    addDate() {
      this.formModel.dates.push({
        date: new Date(),
        details: this.getDefaultDateDetails(),
        uid: Date.now(),
      });
    },
    getDefaultForm() {
      return {
        title: "",
        description: "",
        dates: [],
        dateDetails: {},
      };
    },
    getDefaultDateDetails() {
      return {
        startTime: "",
        endTime: "",
        price: 0,
        type: "",
      };
    },
    deleteItem() {
      this.$emit("delete-shift");
    },
    save() {
      this.$emit("input", this.formModel);
    },
    removeDate(date, hide) {
      this.formModel.dates = this.formModel.dates.filter(
        (d) => d.uid !== date.uid
      );
      if (hide) {
        hide();
      }
    },
    dateSelected(e, date, toggle) {
      this.selectedDate = date;
      toggle();
      e.preventDefault();
      e.stopPropagation();
    },
  },
};
</script>
<style scoped>
:deep(.form-item-full-width .ivu-form-item-label) {
  width: 100% !important;
}
</style>
