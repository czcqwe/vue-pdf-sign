<style src="./annotationLayer.css"></style>
<script>

	import componentFactory from './componentFactory'
	import pdfjsWrapper from './pdfjsWrapper'

	var PDFJS = require('pdfjs-dist/es5/build/pdf.js');

	if ( process.env.VUE_ENV !== 'server' ) {

		if ( typeof window !== 'undefined' && 'Worker' in window ) {

			var PdfjsWorker = require('./pdfWorker.js');
			var PdfjsWorker2 = require('worker-loader!pdfjs-dist/es5/build/pdf.worker.js');
			console.log(PdfjsWorker2,'PdfjsWorker2');
			console.log(PdfjsWorker,'PdfjsWorker');
			console.log(PdfjsWorker.default,'PdfjsWorker');
			PDFJS.GlobalWorkerOptions.workerPort = new PdfjsWorker();
		}
	}

	var component = componentFactory(pdfjsWrapper(PDFJS));
	component.PDFJS = PDFJS;

	export default component;

</script>