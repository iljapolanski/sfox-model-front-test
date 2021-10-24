<template>
  <div class="panel-container">
    <div class="panel">
      <div class="panel-filter">
        <input :placeholder="labels.author" ref="authorName"/>
        <label class="filter-btn" @click="filterByAuthorName">{{ labels.filter }}</label>
      </div>
      <div class="panel-navigation">
        <label class="nav-btn" @click="previousPage">{{ labels.prev }}</label>
        <div class="current-page">{{ currentPage }}</div>
        <label class="nav-btn" @click="nextPage">{{ labels.next }}</label>
      </div>
      <div class="per-page">
        <label :for="numperpage-select">{{ labels.perPage }}</label>
        <select :id="numperpage-select" v-model="numPerPage" @change="setNumPerPage">
          <option v-for="paginationOption in paginationOptions"
                  v-bind:key="paginationOption"
                  v-bind:value="paginationOption"
          >{{ paginationOption }}</option>
        </select>
      </div>
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
      labels: {
        prev: 'Previous',
        next: 'Next',
        perPage: 'Thumbnails per page',
        author: 'Author\'s name',
        filter: 'Filter',
      },
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
@media only screen and (min-width: 1024px) {
  .panel {
    width: 973px;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    .panel-filter {
      border-right: 1px solid whitesmoke;
    }
    .panel-navigation {
      border-right: 1px solid whitesmoke;
    }
  }
}
@media only screen and (min-width: 768px) and (max-width: 1023px) {
  .panel {
    width: 722px;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    .panel-filter {
      border-right: 1px solid whitesmoke;
    }
    .panel-navigation {
      border-right: 1px solid whitesmoke;
    }
  }
}
@media only screen and (max-width: 767px) {
  .panel-container {
    min-width: 312px;
  }
  .panel {
    width: 302px;
    margin: 0px auto;
    flex-direction: column-reverse;
    align-items: flex-end;
    justify-content: center;
    .panel-filter {
      border-right: 0px solid steelblue;
    }
    .panel-navigation {
      border-right: 0px solid steelblue;
    }
  }
}
@mixin unselectable() {
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.panel-container {
  margin: 0px auto;
  padding: 0px;
  display: flex;
  justify-content: center;
}
.panel {
  display: flex;
  background-color: steelblue;
  color: white;
  margin: 5px;
  padding: 4px;
  box-sizing: border-box;
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
      @include unselectable();
      margin: 5px;
      color: whitesmoke;
      text-decoration: none;
      font-size: 12px;
      padding: 5px;
      &:hover {
        background-color: aliceblue;
        color: steelblue;
      }
    }
  }
  .per-page {
    select {
      margin-left: 10px;
      border: 1px solid #ccc;
      background-color: white;
    }
    label {
      @include unselectable();
      font-size: 12px;
      margin-left: 10px;
    }
  }
  .panel-navigation {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    .nav-btn {
      @include unselectable();
      color: whitesmoke;
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
