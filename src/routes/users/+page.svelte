<script lang="ts">
  import { onMount, onDestroy } from "svelte";

  import Table from "$lib/Table.svelte"
  import * as gridjs from "gridjs";

  let sort: boolean = true;
  let url: string = "https://api.subvind.com/users";
  let limit: number = 25;
  let columns = [
    {
      id: 'id',
      name: 'Reference',
      width: '150px',
      sort: false,
      formatter: (cell: any, row: any) => {
        return gridjs.h('div', {
          style: 'width: 70px; white-space: nowrap; overflow: hidden; text-overflow: ellipsis;',
        }, row.cells[0].data);
      }
    },
    {
      id: 'username',
      name: 'Username',
      width: '200px',
    },
    {
      id: 'fullName',
      name: 'Full Name',
      width: '200px',
    },
    {
      id: 'joinDate',
      name: 'Join Date',
      width: '200px',
    },
    { 
      id: 'view',
      name: '',
      width: '100px',
      sort: false,
      hidden: false,
      formatter: (cell: any, row: any) => {
        return gridjs.h('a', {
          href: `/users/${row.cells[1].data}`,
          className: 'btn btn-small yellow black-text lighten-2 right',
        }, 'VIEW');
      }
    },
  ]
  function mapResultsFunc(value: any) {
    return [
      value.id,
      value.username,
      `${value.firstName} ${value.lastName}`,
      value.createdAt
    ]
  }

	onDestroy(() => {
    document.body.classList.remove('no-splash');
  });

	onMount(async () => {
		document.body.classList.add('no-splash');
  })
</script>

<nav class="nav-extended yellow lighten-2">
  <div class="container">
    <div class="nav-wrapper">
      <a href="#" class="brand-logo black-text">Users</a>
    </div>
  </div>
</nav>

<br />
<br />

<div class="container">
  <Table url={url} columns={columns} limit={limit} mapResultsFunc={mapResultsFunc} sort={sort} />
</div>

<br />

<style>
  .dropdown-content {
    width: 200px !important;
  }
</style>