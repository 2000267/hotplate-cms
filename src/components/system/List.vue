<template>
  <div class="list-comp">
    <v-card class="card">
      <v-card-title>
        <h2>{{ props.headerTxt }}</h2>
      </v-card-title>
      <v-card-text>
        <v-row
          v-for="(item, index) in retVal.items"
          :key="index"
          class="item-list"
        >
          <v-col cols="10">
            <v-text-field
              v-model="retVal.items[index]"
              :label="`Item ${index + 1}`"
              filled
            >
            </v-text-field>
          </v-col>
          <v-col cols="2">
            <v-btn color="error" @click="delItem(index)">Delete</v-btn>
          </v-col>
        </v-row>
        <v-btn
          color="secondary"
          class="sectext-text"
          :disabled="reachedMax"
          @click="addItem"
          >Add</v-btn
        >
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
export default {
  name: 'ListComponent',
  props: {
    name: {
      type: String,
      default: ''
    },
    props: {
      type: Object,
      default() {
        return {
          headerTxt: 'List',
          maxItems: 0
        };
      }
    },
    value: {
      type: Object,
      default() {
        return {
          items: []
        };
      }
    }
  },
  data() {
    return {
      retVal: this.value
    };
  },
  computed: {
    reachedMax() {
      if (this.props.maxItems === 0) {
        return false;
      }
      return this.retVal.items.length >= this.props.maxItems;
    }
  },
  created() {
    this.updateData();
  },
  methods: {
    updateData() {
      this.$emit('input', this.retVal);
    },
    addItem() {
      this.retVal.items.push('');
      this.updateData();
    },
    delItem(index) {
      this.retVal.items.splice(index, 1);
      this.updateData();
    }
  }
};
</script>

<style lang="scss">
.list-comp {
  margin: 40px 0;

  .card {
    margin: 0 auto;
  }

  h1 {
    line-height: 2.5rem;
  }

  .item-list {
    text-align: center;
  }
}
</style>
