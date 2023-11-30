<script>
  import { onMount } from 'svelte';
  import { createClient } from '@supabase/supabase-js'

  // Create a single supabase client for interacting with your database
  const supabase = createClient('https://icsokbjfkegzqmymukwh.supabase.co', 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Imljc29rYmpma2VnenFteW11a3doIiwicm9sZSI6ImFub24iLCJpYXQiOjE3MDEyNjA5NTMsImV4cCI6MjAxNjgzNjk1M30.q6yk6q6IBxN5QSxPrxPrJutmH2PcgiHtBHS6qInZTIQ')

  let companies = []

  onMount(async () => {
    const { data, error } = await supabase
      .from('companies')
      .select()
    
      companies = data
	});

</script>

<header>
  <h1>Cleantech companies in India</h1>
</header>
<main>
  <article>
    <table>
      <tbody>
        <tr>
          <th>Name</th>
          <th width="300">Description</th>
          <th>Category</th>
          <th>Year</th>
          <th>Website</th>
        </tr>
        {#each companies as { name, description, category, year, website }}
          <tr>
            <td>{name}</td>
            <td>{description}</td>
            <td>{category}</td>
            <td>{new Date(year)?.getFullYear()}</td>
            <td><a href={website}>{website?.split('www.')[1]?.split('/')[0]}</a></td>
          </tr>
        {/each}
      </tbody>
    </table>
  </article>
</main>

<style>
  table { 
    white-space: initial;
  }

  table td, table th, table tr {
    text-align: initial;
  }
</style>