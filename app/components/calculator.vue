<template>
<UContainer class="q-pa-md" margin: auto;>
  
<h1 class=" text-3xl text-blue-900 uppercase">Calcolatore finanziamento auto</h1>

<UInputNumber v-model="intertesse" placeholder="Interesse in %" class=" m-4"
:step="0.01",
:format-options="{
      minimumFractionDigits: 2,
}" 
/>

<UInputNumber v-model="prezzovettura" placeholder="prezzo vettura" class=" m-4"
:format-options="{
      style: 'currency',
      currency: 'EUR',
      currencyDisplay: 'code',
      currencySign: 'accounting',
      minimumFractionDigits: 1,   
}" label="Prezzo vettura"
/>

<UInputNumber v-model="capitale" placeholder="Capitale da finanziare" class=" m-4"
:format-options="{
      style: 'currency',
      currency: 'EUR',
      currencyDisplay: 'code',
      currencySign: 'accounting',
      minimumFractionDigits: 1,   
}" label="Capitale"
/>

<UInputNumber v-model="giorni" placeholder="Giorni" class=" m-4"
:format-options="{
      style: 'decimal',
      minimumFractionDigits: 0,   
}" label="Giorni"   
/>

<UInputNumber v-model="anni" placeholder="Anni" class=" m-4"/> 
<p>{{ giorniCalcolati }}</p>


<UInputNumber v-model="totaleCostVet" placeholder="Totale" class=" m-4"
:format-options="{
      style: 'currency',
      currency: 'EUR',
      currencyDisplay: 'code',
      currencySign: 'accounting',
      minimumFractionDigits: 2,   
}" readonly
/> <p>Totale costo vettura</p>

<UInputNumber v-model="totInteresse" placeholder="Totale Interesse" class=" m-4"
:format-options="{
      style: 'currency',
      currency: 'EUR',
      currencyDisplay: 'code',
      currencySign: 'accounting',
      minimumFractionDigits: 2,   
}" readonly
/>  <p>Interesse maturato</p>


<div class=" gap-4 mt-5">
      <p>Il costo totale della vettura è di: <span class=" text-orange-700">{{ totaleCostVet.toLocaleString() }}€</span></p>
      <p>L'interesse totale è di €: <span class=" text-orange-500">{{ totInteresse.toLocaleString() }}€</span></p>
</div>
   
</UContainer>

</template>


<script setup >

const intertesse = ref()
const prezzovettura = ref()
const capitale = ref()
const giorni = ref()
const anni = ref()


const giorniCalcolati = computed(() => {
    if (anni.value) {
        return anni.value * 365
    }
    return 0
}) 


const totInteresse = computed(() => {
    if (intertesse.value && capitale.value && giorni.value) {
        return (intertesse.value * capitale.value * giorni.value) / 36500
    }
    return 0
})  

const totaleCostVet  = computed(() => {
    if (intertesse.value && prezzovettura.value && capitale.value && giorni.value) {
        return (prezzovettura.value + totInteresse.value ) 
    }
    return 0
})

</script>