<script>
  export let user;
  export let nestedName;
  const fields = {
    id: "Ид",
    name: "Имя",
    username: "Юзернейм",
    email: "Емейл",
    "address-city": "Город",
    "address-street": "Улица",
    "address-geo-lat": "Долгота",
    "geo-lng": "Широта",
    phone: "Телефон",
  };

  const alias = (v) => (fields[v] ? fields[v] : v);
  $: userfields = Object.entries(user);
</script>

<ul class="list-inside">
  {#each userfields as [key, value]}
    {#if typeof value === 'object'}
      <svelte:self
        user={value}
        nestedName={`${nestedName ? `${nestedName}-` : ''}${key}`} />
    {:else if nestedName}
      <li class="my-1">{alias(`${nestedName}-${key}`)}: {value}</li>
    {:else}
      <li class="my-1">{alias(key)}: {value}</li>
    {/if}
  {/each}
</ul>
