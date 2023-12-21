<template>
	<div>
		<h1>My PDF Viewer</h1>

			<div class="flex flex-row space-x-4 items-center">
				<span>{{ pageNumber.toString() }} /{{ pageCount }}</span>
				<button :id="idConfig.zoomOut" type="button" @click="zoomOut">Zoom out</button>
				<button :id="idConfig.zoomIn" type="button" @click="zoumIn">Zoom in</button>
				<button :id="idConfig.presentationMode" type="button">toggleFullscreen</button>
				<button :id="idConfig.next" type="button" @click="nextPage" >nextpage</button>
				<button :id="idConfig.previous" type="button" @click="prevPage"> previousPage</button>
			</div>
			<PdfApp ref="pdfApp" :pdf="pdfLink" :config="config3" :idConfig="idConfig"  @open="openHandler"  />

		
	</div>
  </template>
<script>

import "vue-pdf-app/dist/icons/main.css";
import PdfApp from "vue-pdf-app";
export default {
components: {
    PdfApp,
  },
  data(){
    return{
        pdfUrl:"https://raw.githubusercontent.com/mozilla/pdf.js/ba2edeae/web/compressed.tracemonkey-pldi-09.pdf",
		idConfig: { 
			zoomIn: "zoomInId", 
			zoomOut: "zoomOutId",
			presentationMode: "presentationModeId",
			next:"next",
			previous:"previous",
			pageNumber:"pageNumber"
		},
        // config: {
		// 	sidebar: {
		// 	viewThumbnail: false,
		// 	viewOutline: false,
		// 	viewAttachments: false,
		// 	},
		// 	findbar: false,
		// 	secondaryToolbar: {
		// 	secondaryPresentationMode: true,
		// 	secondaryOpenFile: true,
		// 	secondaryPrint: true,
		// 	secondaryDownload: true,
		// 	secondaryViewBookmark: true,
		// 	firstPage: true,
		// 	lastPage: true,
		// 	pageRotateCw: true,
		// 	pageRotateCcw: true,
		// 	cursorSelectTool: true,
		// 	cursorHandTool: true,
		// 	scrollVertical: true,
		// 	scrollHorizontal: true,
		// 	scrollWrapped: true,
		// 	spreadNone: true,
		// 	spreadOdd: true,
		// 	spreadEven: true,
		// 	documentProperties: true,
		// 	},
		// 	toolbar: {
		// 	toolbarViewerLeft: {
		// 		previous: true,
		// 		next: true,
		// 		pageNumber: true,
				
		// 	},
		// 	toolbarViewerRight: {
		// 		presentationMode: true,
		// 		openFile: true,
		// 		print: true,
		// 		download: true,
		// 		viewBookmark: true,
		// 		secondaryToolbarToggle: true,
		// 	},
		// 	toolbarViewerMiddle: {
		// 		zoomOut: true,
		// 		zoomIn: true,
		// 		scaleSelectContatiner: true,
		// 	},
		// 	},
		// 	viewerContextMenu: false,
		// 	errorWrapper: true,
     	//  }, 
		info: [] ,
		config3: {
			toolbar: false,
			sidebar:false
		},
		pageCount: 0,
		page:1,
		isFullscreen: false,
		}

  },
  computed: {
    pdfLink() {
      return "https://raw.githubusercontent.com/mozilla/pdf.js/ba2edeae/web/compressed.tracemonkey-pldi-09.pdf";
    },
	pageNumber() {
		return this.page
	}
  },
  methods: {
    async openHandler(pdfApp) {
      this.info = [];
	  console.log(pdfApp.pagesCount)
	  this.page= pdfApp.page
	  this.pageCount = pdfApp.pagesCount
	  console.log(pdfApp.page)
      const info = await pdfApp.pdfDocument
        .getMetadata()
        .catch(console.error.bind(console));

      if (!info) return;
      const props = Object.keys(info.info);
      props.forEach((prop) => {
        const obj = {
          name: prop,
          value: info.info[prop]
        };
        this.info.push(obj);
      });
    },
	test() {
		console.log(this.$refs.pdfApp)
	},
	zoomOut() {
      console.log('zoom out')
    },
    zoomIn() {
		console.log('zoom in')
    },
    toggleFullscreen() {
		console.log('fullscreen')
    },
    nextPage() {
      if (this.page < this.pageCount) {
        this.page += 1;
		console.log('this page number is', this.page)
      }
    },
    prevPage() {
      if (this.page > 1) {
        this.page -= 1;
		console.log('this page number is', this.page)
      }
    },
  }
};
</script>