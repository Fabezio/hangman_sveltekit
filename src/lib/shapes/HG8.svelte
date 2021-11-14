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
	<line id="string" x1="200" x2="200" y1="10" y2="50" stroke={string} stroke-width={strokeWidth} />
	<circle
		id="head"
		cx="200"
		cy={50 + ray}
		r={ray}
		stroke={body}
		fill="transparent"
		stroke-width="3"
	/>
	<line
		id="body"
		x1="200"
		x2="200"
		y1={2 * ray + 50}
		y2={2 * ray + 50 + 90}
		stroke={body}
		stroke-width={strokeWidth}
	/>
	<line
		id="arm-left"
		x1="170"
		x2="200"
		y1="145"
		y2="115"
		stroke={body}
		stroke-width={strokeWidth}
	/>
	<line
		id="arm-right"
		x1="230"
		x2="200"
		y1="145"
		y2="115"
		stroke={body}
		stroke-width={strokeWidth}
	/>
</svg>
