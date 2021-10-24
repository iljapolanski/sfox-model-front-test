<template>
  <div class="panel">
    <div class="panel-filter">
      <input placeholder="Author name" ref="authorName"/>
      <a href="javascript: void(0);" class="filter-btn" @click="filterByAuthorName">Apply</a>
    </div>
    <div class="panel-navigation">
      <a href="javascript: void(0);" class="nav-btn" @click="previousPage">Previous</a>
      <div class="current-page">{{ currentPage }}</div>
      <a href="javascript: void(0);" class="nav-btn" @click="nextPage">Next</a>
    </div>
    <div>
      <select v-model="numPerPage" @change="setNumPerPage">
        <option v-for="paginationOption in paginationOptions"
                v-bind:key="paginationOption"
                v-bind:value="paginationOption"
        >{{ paginationOption }}</option>
      </select>
    </div>
  </div>
</template>

<script>
export default {
  name: "ToolsPanel",
  props: {
    currentPage: Number,
  },
  data() {
    return {
      numPerPage: 30,
      paginationOptions: [4, 8, 16, 30, 60, 100],
    };
  },
  methods: {
    previousPage() {
      this.$emit('prev');
    },
    nextPage() {
      this.$emit('next');
    },
    setNumPerPage() {
      this.$emit('paginate', {pagination: this.numPerPage});
    },
    filterByAuthorName() {
      this.$emit('search', {search: this.$refs.authorName.value});
    },
  },
}
</script>

<style scoped lang="scss">
@media only screen and (min-width: 768px) {
  .panel {
    flex-direction: row;
    align-items: center;
    justify-content: center;
    .panel-filter {
      border-right: 1px solid steelblue;
    }
    .panel-navigation {
      border-right: 1px solid steelblue;
    }
  }
}
@media only screen and (max-width: 768px) {
  .panel {
    width: 300px;
    margin: 0px auto;
    flex-direction: column-reverse;
    align-items: flex-end;
    justify-content: flex-end;
    .panel-filter {
      border-right: 0px solid steelblue;
    }
    .panel-navigation {
      border-right: 0px solid steelblue;
    }
  }
}
.panel {
  display: flex;
  .panel-filter {
    display: flex;
    flex-direction: row;
    align-items: center;
    input {
      margin: 5px;
      border: 1px solid #ccc;
      padding: 5px;
    }
    .filter-btn {
      margin: 5px;
      color: black;
      text-decoration: none;
      font-size: 12px;
      padding: 5px;
      &:hover {
        background-color: aliceblue;
        color: steelblue;
      }
    }
  }
  select {
    margin-left: 10px;
    border: 1px solid #ccc;
    background-color: white;
  }
  .panel-navigation {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    .nav-btn {
      color: black;
      padding-right: 5px;
      padding-left: 5px;
      padding-bottom: 5px;
      padding-top: 5px;
      text-decoration: none;
      font-size: 12px;
      margin: 5px;
    }
    .nav-btn:hover {
      color: steelblue;
      background-color: aliceblue;
    }
    .current-page {
      padding-left: 10px;
      padding-right: 10px;
      border: 1px solid #ccc;
    }
  }
}
</style>
