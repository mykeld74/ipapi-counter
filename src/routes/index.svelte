<script>
	const checkIpApiUsage = (async () => {
		const response = await fetch(
			'https://ipapi.co/quota/?key=rLBVazTbhCesxEGft6N3aI0Cu6Q7Wbhwe5jSkAYPAFnw6o7NLE'
		);
		return await response.json();
	})();

	const logo = '/suited-connector-logo.png';
</script>

<svelte:head>
	<title>SuCo IpAPI Counter</title>
</svelte:head>
<header><div class="logo"><img src={logo} alt="SuCo Logo" /></div></header>
<main>
	<div class="intro">
		<p class="underline">SuCo ipapi.co usage:</p>
		{#await checkIpApiUsage}
			<p>...checking</p>
		{:then data}
			<p class="used">
				We have made <span class="number">{(15000000 - data.available).toLocaleString()}</span> requests.
			</p>
			<p class-="unused">
				We have <span class="number">{data.available.toLocaleString()}</span> requests remaining.
			</p>
		{:catch error}
			<p>It looks like something went wrong!</p>
		{/await}
		<hr />
		<p>
			To see which sites are currently white listed go <a
				href="https://ipapi.co/account/#settings"
				target="_blank"
				rel="noopener noreferrer">here</a
			>
		</p>
	</div>
</main>

<style>
	header {
		background: #dedede;
		padding: 20px 0;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	main {
		width: 960px;
		max-width: 100%;
		padding: 15px;
		margin: 0 auto;
	}
	.logo {
		width: 150px;
	}
	p {
		font-size: clamp(18px, 3vw, 28px);
		line-height: 1.5;
		margin: 0;
	}

	.number {
		font-weight: 700;
		color: red;
	}
	.underline {
		text-decoration: underline;
		font-weight: 700;
	}
</style>
