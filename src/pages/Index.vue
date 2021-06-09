<template>
  <q-page padding>
  <q-table
      title="Data Kegiatan"
      :data="data"
      :columns="columns"
      row-key="namaKegiatan"
    >
      <template v-slot:top-right>
        <q-btn
          icon="add_box"
          label="Input Kegiatan"
          unelevated
          color="primary"
          :to="{ name:'inputKegiatan' }"
        />
      </template>
      <template v-slot:body="props">
        <q-tr :props="props">
          <q-td key="namaKegiatan" :props="props">
            {{ props.row.namaKegiatan }}
          </q-td>
          <q-td key="deskripsi" :props="props">
            {{ props.row.deskripsi }}
          </q-td>
          <q-td key="waktu" :props="props">
            {{ props.row.waktu }}
          </q-td>
          <q-td key="aksi" :props="props">
            <q-btn
              label = "Edit"
              icon = "edit"
              color = "warning"
              unelevated
            />
            <q-btn
              label = "Hapus"
              icon = "delete"
              color = "negative"
              class = "q-ml-md"
              unelevated
            />
          </q-td>
        </q-tr>
      </template>
    </q-table>
  </q-page>
</template>

<script>
export default {
  data(){
    return{
      columns: [
        {
           name: 'namaKegiatan',
           align: 'left',
           label: 'nama Kegiatan',
           field: 'namaKegiatan'
        },
        {
           name: 'deskripsi',
           align: 'left',
           label: 'Deskripsi',
           field: 'deskripsi'
        },
        {
           name: 'waktu',
           align: 'left',
           label: 'Waktu',
           field: 'waktu'
        },
        {
           name: 'aksi',
           align: 'left',
           label: 'Aksi',
           field: 'aksi'
        }
      ],
      data: [],
    }
  },
  created () {
    this.getData()
  },
  methods: {
    getData () {
      this.$axios.get('kegiatan/getall')
        .then(res =>{
          this.data = res.data.result
        })
    }
  }
}
</script>
