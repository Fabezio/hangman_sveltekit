<!-- <?xml version="1.0" standalone="no"?> -->
<script>
	const strokeWidth = '3';
	const wood = 'sienna';
	const string = '#756';
	const body = 'salmon';
	const stringLength = 40;
	const ray = 20;
</script>

<svg width="250" height="250" version="1.1" xmlns="http://www.w3.org/2000/svg">
	<line id="base" x1="10" x2="110" y1="240" y2="240" stroke={wood} stroke-width={strokeWidth} />
	<line id="mast" x1="60" x2="60" y1="240" y2="10" stroke={wood} stroke-width={strokeWidth} />
	<line id="beam" x1="60" x2="200" y1="10" y2="10" stroke={wood} stroke-width={strokeWidth} />
	<line id="framekey" x1="60" x2="90" y1="40" y2="10" stroke={wood} stroke-width={strokeWidth} />
</svg>
