<script lang="ts">
    import Input from '$lib/Input.svelte';
    import Table from '$lib/Table.svelte';
    import TableAction from '$lib/TableAction.svelte';
</script>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>

<!-- <Input type="password" /> -->

<Table heads={['Name', 'Age', 'Actions']} component={TableAction} rows={[
    ['Are John', '25', {html:`<button onclick="alert()">OK</button>`}],
    ['Laku Kane', '26', 'string'],
    ['Mane Joe', '27', {svelte: 'myfunc'}],
    ['Bae Dack', '28'],
    ['Lao Kill', '29'],

    ['Kas Staven', '40'],
    ['Tare Lloyd', '12'],
    ['Gurd John', '25'],
    ['Pan Kane', '26'],
    ['Fol Joe', '27'],
    
    ['Bar Dack', '28'],
    ['Olim Kill', '29'],
    ['Xo Staven', '40'],
    ['Dan Lloyd', '12'],
    ['John Doe', '25'],
    
    ['Kane Jo', '26'],
    ['Joe Xi', '27'],
    ['Dack Pa', '28'],
    ['Kill Bee', '29'],
    ['Staven Yu', '40'],
    
    ['Lloyd Mark', '12'],
]} />