<script>
	import ClipboardJS from 'clipboard';
	import sanitizeHTML from 'sanitize-html';

	new ClipboardJS('.clipboardjs-button');

	$: chunk = "";
	// let defaultAllowedTags = [ 'p', 'b', 'i', 'em', 'strong', 'img', 'a', 'br' ];
	let defaultAllowedTags = [
		'img', 'p', 'a', 'b', 'i', 'strong', 'em', 'hr', 'br', 'div',
		'table', 'thead', 'tbody', 'tr', 'th', 'td'
	];
	$: myAllowedTags = defaultAllowedTags;
	$: cleanedUp = sanitizeHTML(chunk,{
		allowedTags: myAllowedTags,
  	allowedAttributes: {
    	'a': [ 'href', 'target' ],
			'img': ['src'],
			'span': ['style'],
			'table': ['width'],
			'p': ['style']
  	},
		allowedStyles: {
			'*': {
				'color': [/^#(0x)?[0-9a-f]+$/i, /^rgb\(\s*(\d{1,3})\s*,\s*(\d{1,3})\s*,\s*(\d{1,3})\s*\)$/],
				'text-align': [/^center$/]
			}
		},
		exclusiveFilter: function(frame) {
      return frame.tag === 'p' && !frame.text.trim();
    }
	}).trim();
	
	let exampledirty2 = `<meta charset="utf-8">
<meta charset="utf-8"><p><span style="background-color: #ddd; color: #ff0000;"><strong><a href="http://hazelvillage.com/" style="color: #ff0000;">Hazel Village</a> + WWF</strong> Limited Edition Item</span></p>
<p>Owen Fox in his In The Forest Navy romper is part of a limited-edition collaboration with our friends at Hazel Village. </p>
<div>To see matching outfits for little humans, click <a href="https://www.winterwaterfactory.com/collections/in-the-forest" target="_blank" title="Hazel Village + Winter Water Factory matching prints" rel="noopener noreferrer">here</a>.<br> <br> ABOUT OWEN FOX<br> <b><br></b><meta charset="utf-8">
<span>Owen loves to go to his secret tree house and practice his dance moves. He says he's such a nimble dancer because he has a low center of gravity. But the other animals, who have similarly low centers of gravity, say he just has a lot of energy.</span><br> <br><meta charset="utf-8">
<span>He is made of organic cotton fleece, with white fleece on his nose and tail. He measures about 15 inches, ear to toe. He is stuffed with washable fiberfill. His eyes, nose, and whiskers are hand embroidered with cotton thread. If and when he gets scuffed or grimy, he can be hand-washed and he will air dry.</span><br>
</div><div>new</div>`;

	let exampledirty = `<meta charset="utf-8">
<p>Their new favorite pants in our <span data-sheets-value='{"1":2,"2":"Bug Collection print! A gallery of insects that would make any tiny entomologist proud."}' data-sheets-userformat='{"2":14849,"3":{"1":0},"12":0,"14":{"1":2,"2":2173750},"15":"-apple-system, system-ui, \"San Francisco\", Roboto, \"Segoe UI\", \"Helvetica Neue\", sans-serif","16":11}'>Bug Collection print! A gallery of insects that would make any tiny entomologist proud.</span></p>
<p>Our Harem pants are the perfect style for lounge or play! They have a soft elastic waist and slight drop-crotch style. Stylish and so comfortable.</p>
<p>-Made in Brooklyn NY USA<br><br>-100% Certified Organic Cotton</p>
<style type="text/css"><!--
td {border: 1px solid #ccc;}br {mso-data-placement:same-cell;}
--></style>
<style type="text/css"><!--
td {border: 1px solid #ccc;}br {mso-data-placement:same-cell;}
--></style>
<style type="text/css"><!--
td {border: 1px solid #ccc;}br {mso-data-placement:same-cell;}
--></style>
<style type="text/css"><!--
td {border: 1px solid #ccc;}br {mso-data-placement:same-cell;}
--></style>
<style type="text/css"><!--
td {border: 1px solid #ccc;}br {mso-data-placement:same-cell;}
--></style>`;

	let exampledirty3 = `<div>A long summer dress <meta charset="utf-8">
<meta charset="utf-8">
<span><span>in our</span></span><span> In The Garden print, designed exclusively for Winter Water Factory by <a href="http://www.emilyisabella.com/" target="_blank" title="Emily Isabella" rel="noopener noreferrer">Emily Isabella</a>.</span>
</div>
<div><br></div>
<div>The Idaho dress falls below the knee, and is cut generously, giving it a cozy and airy feel. Gathered at the natural waist, it flows from the shoulders - and it has pockets! Transitions easily into fall with a cardigan. <br>
</div>
<div><br></div>
<div>Runs slightly large, so we recommend sizing down.</div>
<div><br></div>
<div>
<p><span class="gmail-s1">-Made in Brooklyn NY USA</span></p>
<p><span class="gmail-s1">-100% Certified Organic Cotton</span></p>
<p><span>Model is 5'6" and is wearing size S.</span></p>
</div>
<meta charset="utf-8">
<p style="text-align: center;"><strong>Garment Measurements:</strong><br></p>
<meta charset="utf-8">
<table width="100%">
<tbody>
<tr>
<td></td>
<td><strong>CHEST</strong></td>
<td><strong>WAIST</strong></td>
<td><strong>LENGTH</strong></td>
</tr>
<tr>
<td>
<p><strong>XS</strong></p>
</td>
<td>18"</td>
<td>18"</td>
<td>44.5"</td>
</tr>
<tr>
<td><strong>S</strong></td>
<td>19"</td>
<td>19"</td>
<td>45"</td>
</tr>
<tr>
<td><strong>M</strong></td>
<td>20"</td>
<td>20"</td>
<td>45.5"</td>
</tr>
<tr>
<td><strong>L</strong></td>
<td>21.5"</td>
<td>21.5"</td>
<td>46"</td>
</tr>
<tr>
<td><strong>XL</strong></td>
<td>23"</td>
<td>23"</td>
<td>46.5"</td>
</tr>
<tr>
<td><strong>XXL</strong></td>
<td>24.5"</td>
<td>24.5"</td>
<td>47"</td>
</tr>
<tr>
<td><strong>XXXL</strong></td>
<td>26"</td>
<td>26"</td>
<td>47.5"</td>
</tr>
</tbody>
</table>`;
</script>

<div class="container">
	<div class="columns">
		<div class="column col-12">
			<h1 class="d-inline light">clean up html</h1>
			<p class="d-inline">Paste messy html into <i>input</i>, Copy the cleaned html from <i>output</i>.</p>
			<p></p>
			<label for="myAllowed">Allow only these tags in output. <i>text inside of all tags is preserved.</i></label>
			<button class="btn btn-link" on:click={()=>{return myAllowedTags=defaultAllowedTags}}> reset</button>
			<textarea rows="1" type="text" name="myAllowed" bind:value={myAllowedTags}></textarea>
		</div>
		<div class="column col-12">
			<div class="divider"></div>
		</div>
		<div class="column col-6">
			<div class="wrapper wrapper-in">
				<h2 class="d-inline light">input</h2>
				<button class="btn btn-link" on:click={()=>{chunk=exampledirty}}>sample1</button>
				<button class="btn btn-link" on:click={()=>{chunk=exampledirty2}}>sample2</button>
				<button class="btn btn-link" on:click={()=>{chunk=exampledirty3}}>sample3</button>
				<button class="btn btn-link" on:click={()=>{chunk=""}}>clear</button>
			</div>
			<textarea rows="16" cols="33" class="dirty" bind:value={chunk}></textarea>
		</div>
		<div class="column col-6">
			<div class="wrapper wrapper-out">
				<h2 class="d-inline light">output</h2>
				<button class="clipboardjs-button btn btn-link" data-clipboard-target="#output">
					copy to clipboard
				</button>
			</div>
			<textarea id="output" rows="16" cols="33" class="cleaned" bind:value={cleanedUp}></textarea>
		</div>
		<div class="column col-12 mb-2 pb-2">

			<!-- <div class="divider"></div> -->
		</div>
		<div class="column col-6">
			<h2 class="light">HTML preview</h2>
			<div class="html_preview">
				{@html chunk}</div>
		</div>
		<div class="column col-6">
			<h2 class="light">HTML preview</h2>
			<div class="html_preview">
				{@html cleanedUp}</div>
		</div>
	</div>
</div>
<div class="container">
	<div class="info">made with <a class="infolink" href="https://svelte.dev/">&nbsp;Svelte</a>,&nbsp;<a class="infolink" href="https://github.com/apostrophecms/sanitize-html#readme"> sanitize-html</a>, &amp;&nbsp; <a class="infolink" href="https://github.com/zenorocha/clipboard.js#readme"> clipboard.js</a>
	</div>
</div>


