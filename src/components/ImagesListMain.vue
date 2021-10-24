<template>
  <div class="main">
    <!-- Tools panel with search by author name, navigation, pagination -->
    <tools-panel :currentPage="currentPage"
      @next="nextPage"
      @prev="previousPage"
      @search="filterByAuthorName"
      @paginate="setNumPerPage"
    />

    <!-- Main section with thumbnails -->
    <div class="thumbs-container">
      <thumb v-for="img in currentImagesList"
       :key="img.id"
       :author="img.author"
       :id="img.id"
       :responsive-url="img.thumbnailUrl"
       :src-url="img.previewUrl"
       @onClick="showThumbPreviewPopup"
      />
    </div>

    <!-- Modal popup with image preview -->
    <modal v-if="isPopupVisible" :popup-src="popupSrc" @onHide="hidePopup"/>
  </div>
</template>

<script>
import Thumb from "./Thumb";
import Modal from "./Modal";
import ToolsPanel from "./ToolsPanel";
import urlConstants from '../api/constants';
export default {
  name: 'ImagesListMain',
  components: {
    ToolsPanel,
    Modal,
    Thumb,
  },
  data() {
    return {
      imagesList: [],
      currentPage: 1,
      popupSrc: '',
      isPopupVisible: false,
      searchString: '',
    };
  },
  computed: {
    currentImagesList() {
      const searchString = this.searchString;
      if (searchString.length === 0) {
        return this.imagesList;
      }
      return this.imagesList.filter(img => (img.author.length) ? img.author.indexOf(searchString) !== (-1) : false);
    },
  },
  methods: {
    getImagesList() {
      const options = {
        params: {
          page: this.currentPage,
          limit: this.numPerPage,
        },
      };
      const axios = require('axios').default;
      axios.get(urlConstants.LIST_URL, options)
      .then(response => {
        if (response.data.length === 0) {
          this.currentPage--;
          this.getImagesList();
          return;
        }
        this.imagesList = response.data.map(img => {
          img.thumbnailUrl = `${urlConstants.ITEM_URL}${img.id}/367/267`;
          if (window.document.body.offsetWidth < 768) {
            img.previewUrl = `${urlConstants.ITEM_URL}${img.id}/320/240`;
          } else {
            img.previewUrl = `${urlConstants.ITEM_URL}${img.id}/1024/786`;
          }
          return img;
        });
      });
    },
    filterByAuthorName(payload) {
      this.searchString = payload.search;
    },
    previousPage() {
      this.currentPage--;
      this.currentPage = (this.currentPage <= 0) ? 1: this.currentPage;
      this.getImagesList();
    },
    nextPage() {
      this.currentPage++;
      this.getImagesList();
    },
    setNumPerPage(payload) {
      this.numPerPage = payload.pagination;
      this.currentPage = 1;
      this.getImagesList();
    },
    showThumbPreviewPopup(payload) {
      this.popupSrc = payload.srcUrl;
      this.isPopupVisible = true;
    },
    hidePopup() {
      this.isPopupVisible = false;
    },
  },
  mounted: function () {
    this.getImagesList();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.thumbs-container {
  width: 320px;
  max-width: 320px;
  margin: 0px auto;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
}
@media only screen and (min-width: 768px) {
  .thumbs-container {
    width: 1000px;
    max-width: 1000px;
  }
}
</style>
