<script>
  import { tick } from "svelte";
  import Example1 from './Example1.svelte';
  import Example2 from './Example2.svelte';
  import 'moment/locale/fr';
  import moment from 'moment';

  moment.locale('fr');
  const localStorage = window.localStorage;

  let style = localStorage.getItem("style") || "jb";
  let title = localStorage.getItem("title") || "VT00022";
  let quantity = localStorage.getItem("quantity") || 21;
  let price_without_vat = localStorage.getItem("price_without_vat") || 540;
  $: price_without_vat_value = new Intl.NumberFormat("fr-FR", {
    style: "currency",
    currency: "EUR"
  }).format(price_without_vat);

  let vat = localStorage.getItem("vat") || 20;
  let designation = localStorage.getItem("designation") || "Réalisation d'une prestation de service";

  let start_date_facturation_value = new Date(new Date().getFullYear(), new Date().getMonth(), 1);
  $: start_date_facturation = moment(start_date_facturation_value).format('DD/MM');

  let end_date_facturation_value  = new Date(new Date().getFullYear(), new Date().getMonth() + 1, 0);
  $: end_date_facturation = moment(end_date_facturation_value).format('DD/MM');

  let date_simple_fr_value = new Date().toDateString();
  $: date_simple_fr = new Date(date_simple_fr_value).toLocaleDateString();
  $: date_full_fr = moment(date_simple_fr_value).format('dddd D MMMM YYYY');

  $: year = new Date(date_simple_fr_value).getFullYear();
  $: date_simple_fr_60_days = new Date(
    new Date(date_simple_fr_value).getFullYear(),
    new Date(date_simple_fr_value).getMonth(),
    new Date(date_simple_fr_value).getDate() + 60
  ).toLocaleDateString();

  $: total_without_vat_value = quantity * price_without_vat;
  $: price_of_vat_value = total_without_vat_value * (vat / 100.0);
  $: total_with_vat_value = total_without_vat_value + price_of_vat_value;

  $: price_of_vat = new Intl.NumberFormat("fr-FR", {
    style: "currency",
    currency: "EUR"
  }).format(price_of_vat_value);
  $: total_without_vat = new Intl.NumberFormat("fr-FR", {
    style: "currency",
    currency: "EUR"
  }).format(total_without_vat_value);
  $: total_with_vat = new Intl.NumberFormat("fr-FR", {
    style: "currency",
    currency: "EUR"
  }).format(total_with_vat_value);

  let myCompany = {
    name: localStorage.getItem("company-name") || "",
    contact: localStorage.getItem("company-contact") || "",
    declaraction: localStorage.getItem("company-declaraction") || "",
    registration: localStorage.getItem("company-registration") || "",
    siret: localStorage.getItem("company-siret") || "",
    address: localStorage.getItem("company-address") || "",
    cp: localStorage.getItem("company-cp") || "",
    tel: localStorage.getItem("company-tel") || "",
    email: localStorage.getItem("company-email") || "",
    iban: localStorage.getItem("company-iban") || "",
    swift: localStorage.getItem("company-swift") || "",
  };

  let customer = {
    name: localStorage.getItem("customer-name") || "",
    address: localStorage.getItem("customer-address") || "",
    cp: localStorage.getItem("customer-cp") || "",
    commandNumber: localStorage.getItem("customer-commandNumber") || "",
    affaireNumber: localStorage.getItem("customer-affaireNumber") || "",
    finalClient: localStorage.getItem("customer-finalClient") || "",
  };

  function saveInformations() {
    localStorage.setItem("company-name", myCompany.name);
    localStorage.setItem("company-contact", myCompany.contact);
    localStorage.setItem("company-declaraction", myCompany.declaraction);
    localStorage.setItem("company-registration", myCompany.registration);
    localStorage.setItem("company-siret", myCompany.siret);
    localStorage.setItem("company-address", myCompany.address);
    localStorage.setItem("company-cp", myCompany.cp);
    localStorage.setItem("company-tel", myCompany.tel);
    localStorage.setItem("company-email", myCompany.email);
    localStorage.setItem("company-iban", myCompany.iban);
    localStorage.setItem("company-swift", myCompany.swift);

    localStorage.setItem("customer-name", customer.name);
    localStorage.setItem("customer-address", customer.address);
    localStorage.setItem("customer-cp", customer.cp);
    localStorage.setItem("customer-commandNumber", customer.commandNumber);
    localStorage.setItem("customer-affaireNumber", customer.affaireNumber);
    localStorage.setItem("customer-finalClient", customer.finalClient);

    localStorage.setItem("style", style);

    localStorage.setItem("title", title);
    localStorage.setItem("quantity", quantity);
    localStorage.setItem("price_without_vat", price_without_vat);
    localStorage.setItem("vat", vat);
    localStorage.setItem("designation", designation);

    alert("Informations saved ! ✌");
  }

  $: print = false;
  const toggle = () => (print = !print);
  const windowPrint = () => window.print();
  async function printDocument() {
    focused = '';
    toggle();
    await tick();
    windowPrint();
    await tick();
    toggle();
  }

  $: showGeneral = true;
  function toggleGeneral() {
    showGeneral = !showGeneral;
  }

  let showEntrepriseInit = !(
    myCompany.name
    && myCompany.declaraction
    && myCompany.contact
    && myCompany.registration
    && myCompany.siret
    && myCompany.address
    && myCompany.cp
    && myCompany.tel
    && myCompany.email
    && myCompany.iban
    && myCompany.swift
  );

  $: showEntreprise = showEntrepriseInit;
  function toggleEntreprise() {
    showEntreprise = !showEntreprise;
  }

  let showClientInit = !(
    customer.name
    && customer.address
    && customer.cp
    && customer.commandNumber
    && customer.affaireNumber
    && customer.finalClient
  );

  $: showClient = showClientInit;
  function toggleClient() {
    showClient = !showClient;
  }

  $: focused = '';
  function onFocus(e) {
    focused = e.target.id;
  }

  function onFocusOut() {
    focused = '';
  }
</script>

{#if !print}
  <div class="controls">
    <div class="box {showGeneral ? '' : 'is-paddingless'}">
      <div class="has-icons-left hoverable" on:click={toggleGeneral}>
        <span class="icon is-right">
          <i class="fas fa-address-book" />
        </span>
        General
      </div>

      {#if showGeneral}
      <div class="field">
          <label for="title" class="label is-small">Titre</label>
          <div class="control has-icons-right">
            <input
              id="title"
              type="text"
              on:focus={onFocus}
              on:focusout={onFocusOut}
              bind:value={title}
              placeholder="Title of the document"
              class="input is-small {title ? 'is-success' : 'is-danger'}" />
            <span class="icon is-small is-right">
              <i class="fas fa-check" />
            </span>
          </div>
        </div>

      <div class="field">
          <label class="label is-small" for="date_simple_fr">
            Date d'émision
          </label>
          <div class="control has-icons-right">
            <input
              id="date_simple_fr"
              type="date"
              on:focus={onFocus}
              on:focusout={onFocusOut}
              bind:value={date_simple_fr_value}
              placeholder="Facture date"
              class="input is-small {date_simple_fr_value ? 'is-success' : 'is-danger'}" />
            <span class="icon is-small is-right">
              <i class="fas fa-check" />
            </span>
          </div>
        </div>

      <div class="field">
          <label class="label is-small" for="vat">TVA</label>
          <div class="control has-icons-right">
            <input
              id="vat"
              type="number"
              on:focus={onFocus}
              on:focusout={onFocusOut}
              bind:value={vat}
              placeholder="The VAT"
              class="input is-small {vat ? 'is-success' : 'is-danger'}" />
            <span class="icon is-small is-right">
              <i class="fas fa-check" />
            </span>
          </div>
        </div>

      <div class="field">
          <label class="label is-small" for="quantity">
            Quantité jours/homme
          </label>
          <div class="control has-icons-right">
            <input
              id="quantity"
              type="number"
              on:focus={onFocus}
              on:focusout={onFocusOut}
              bind:value={quantity}
              placeholder="The quantity"
              class="input is-small {quantity ? 'is-success' : 'is-danger'}" />
            <span class="icon is-small is-right">
              <i class="fas fa-check" />
            </span>
          </div>
        </div>

      <div class="field">
          <label class="label is-small" for="price_without_vat">
            Prix par jour HT
          </label>
          <div class="control has-icons-right">
            <input
              id="price_without_vat"
              type="number"
              on:focus={onFocus}
              on:focusout={onFocusOut}
              bind:value={price_without_vat}
              placeholder="The price without VAT"
              class="input is-small {price_without_vat ? 'is-success' : 'is-danger'}" />
            <span class="icon is-small is-right">
              <i class="fas fa-check" />
            </span>
          </div>
        </div>

      <div class="field">
        <label class="label is-small" for="designation">
          Designation
        </label>
        <div class="control has-icons-right">
          <input
                  id="designation"
                  type="text"
                  on:focus={onFocus}
                  on:focusout={onFocusOut}
                  bind:value={designation}
                  placeholder="The designation"
                  class="input is-small {designation ? 'is-success' : 'is-danger'}" />
          <span class="icon is-small is-right">
              <i class="fas fa-check" />
            </span>
        </div>
      </div>

      <div class="field">
        <label class="label is-small" for="start_date_facturation">
          Début de facturation
        </label>
        <div class="control has-icons-right">
          <input
                  id="start_date_facturation"
                  type="date"
                  on:focus={onFocus}
                  on:focusout={onFocusOut}
                  bind:value={start_date_facturation_value}
                  placeholder="Début de facturation"
                  class="input is-small {start_date_facturation_value ? 'is-success' : 'is-danger'}" />
          <span class="icon is-small is-right">
              <i class="fas fa-check" />
            </span>
        </div>
      </div>

      <div class="field">
        <label class="label is-small" for="end_date_facturation">
          Fin de facturation
        </label>
        <div class="control has-icons-right">
          <input
                  id="end_date_facturation"
                  type="date"
                  on:focus={onFocus}
                  on:focusout={onFocusOut}
                  bind:value={end_date_facturation_value}
                  placeholder="Fin de facturation"
                  class="input is-small {end_date_facturation_value ? 'is-success' : 'is-danger'}" />
          <span class="icon is-small is-right">
              <i class="fas fa-check" />
            </span>
        </div>
      </div>

      <div class="field">
        <label class="label is-small">
          Style
        </label>
        <div class="control">
          <label class="radio">
            <input type="radio" name="jb" bind:group={style} value="jb">
            JB
          </label>
          <label class="radio">
            <input type="radio" name="henri" bind:group={style} value="henri">
            Henri
          </label>
        </div>
      </div>
      {/if}
    </div>

    <div class="box {showEntreprise ? '' : 'is-paddingless'}">
      <div class="has-icons-left hoverable" on:click={toggleEntreprise}>
        <span class="icon is-right">
          <i class="fas fa-city" />
        </span>
        Entreprise
      </div>

      {#if showEntreprise}
        <div class="field">
          <label class="label is-small" for="myCompany-name">
            Nom de l'entrepise
          </label>
          <div class="control has-icons-right">
            <input
              id="myCompany-name"
              type="text"
              on:focus={onFocus}
              on:focusout={onFocusOut}
              bind:value={myCompany.name}
              placeholder="Company name of the document"
              class="input is-small {myCompany.name ? 'is-success' : 'is-danger'}" />
            <span class="icon is-small is-right">
              <i class="fas fa-check" />
            </span>
          </div>
        </div>

      <div class="field">
        <label class="label is-small" for="myCompany-contact">
          Contact de l'entrepise
        </label>
        <div class="control has-icons-right">
          <input
                  id="myCompany-contact"
                  type="text"
                  on:focus={onFocus}
                  on:focusout={onFocusOut}
                  bind:value={myCompany.contact}
                  placeholder="Company contact of the document"
                  class="input is-small {myCompany.contact ? 'is-success' : 'is-danger'}" />
          <span class="icon is-small is-right">
              <i class="fas fa-check" />
            </span>
        </div>
      </div>

      <div class="field">
        <label class="label is-small" for="myCompany-declaraction">
          Declaraction de l'entrepise
        </label>
        <div class="control has-icons-right">
          <input
                  id="myCompany-declaraction"
                  type="text"
                  on:focus={onFocus}
                  on:focusout={onFocusOut}
                  bind:value={myCompany.declaraction}
                  placeholder="Company declaraction of the document"
                  class="input is-small {myCompany.declaraction ? 'is-success' : 'is-danger'}" />
          <span class="icon is-small is-right">
              <i class="fas fa-check" />
            </span>
        </div>
      </div>

      <div class="field">
        <label class="label is-small" for="myCompany-registration">
          Registration de l'entrepise
        </label>
        <div class="control has-icons-right">
          <input
                  id="myCompany-registration"
                  type="text"
                  on:focus={onFocus}
                  on:focusout={onFocusOut}
                  bind:value={myCompany.registration}
                  placeholder="Company registration of the document"
                  class="input is-small {myCompany.registration ? 'is-success' : 'is-danger'}" />
          <span class="icon is-small is-right">
              <i class="fas fa-check" />
            </span>
        </div>
      </div>

      <div class="field">
        <label class="label is-small" for="myCompany-siret">
          SIRET de l'entrepise
        </label>
        <div class="control has-icons-right">
          <input
                  id="myCompany-siret"
                  type="text"
                  on:focus={onFocus}
                  on:focusout={onFocusOut}
                  bind:value={myCompany.siret}
                  placeholder="Company siret of the document"
                  class="input is-small {myCompany.siret ? 'is-success' : 'is-danger'}" />
          <span class="icon is-small is-right">
              <i class="fas fa-check" />
            </span>
        </div>
      </div>

        <div class="field">
          <label class="label is-small" for="myCompany-address">
            Addresse de l'entreprise
          </label>
          <div class="control has-icons-right">
            <input
              id="myCompany-address"
              type="text"
              on:focus={onFocus}
              on:focusout={onFocusOut}
              bind:value={myCompany.address}
              placeholder="Company address of the document"
              class="input is-small {myCompany.address ? 'is-success' : 'is-danger'}" />
            <span class="icon is-small is-right">
              <i class="fas fa-check" />
            </span>
          </div>
        </div>

        <div class="field">
          <label class="label is-small" for="myCompany-cp">Code Postale</label>
          <div class="control has-icons-right">
            <input
              id="myCompany-cp"
              type="text"
              on:focus={onFocus}
              on:focusout={onFocusOut}
              bind:value={myCompany.cp}
              placeholder="Company cp of the document"
              class="input is-small {myCompany.cp ? 'is-success' : 'is-danger'}" />
            <span class="icon is-small is-right">
              <i class="fas fa-check" />
            </span>
          </div>
        </div>

        <div class="field">
          <label class="label is-small" for="myCompany-tel">Téléphone</label>
          <div class="control has-icons-right">
            <input
              id="myCompany-tel"
              type="text"
              on:focus={onFocus}
              on:focusout={onFocusOut}
              bind:value={myCompany.tel}
              placeholder="Company tel of the document"
              class="input is-small {myCompany.tel ? 'is-success' : 'is-danger'}" />
            <span class="icon is-small is-right">
              <i class="fas fa-check" />
            </span>
          </div>
        </div>

        <div class="field">
          <label class="label is-small" for="myCompany-email">Email</label>
          <div class="control has-icons-right">
            <input
              id="myCompany-email"
              type="text"
              on:focus={onFocus}
              on:focusout={onFocusOut}
              bind:value={myCompany.email}
              placeholder="Company email of the document"
              class="input is-small {myCompany.email ? 'is-success' : 'is-danger'}" />
            <span class="icon is-small is-right">
              <i class="fas fa-check" />
            </span>
          </div>
        </div>

        <div class="field">
        <label class="label is-small" for="myCompany-iban">IBAN</label>
        <div class="control has-icons-right">
          <input
                  id="myCompany-iban"
                  type="text"
                  on:focus={onFocus}
                  on:focusout={onFocusOut}
                  bind:value={myCompany.iban}
                  placeholder="Company iban of the document"
                  class="input is-small {myCompany.iban ? 'is-success' : 'is-danger'}" />
          <span class="icon is-small is-right">
              <i class="fas fa-check" />
            </span>
        </div>
      </div>

        <div class="field">
        <label class="label is-small" for="myCompany-swift">SWIFT</label>
        <div class="control has-icons-right">
          <input
                  id="myCompany-swift"
                  type="text"
                  on:focus={onFocus}
                  on:focusout={onFocusOut}
                  bind:value={myCompany.swift}
                  placeholder="Company swift of the document"
                  class="input is-small {myCompany.swift ? 'is-success' : 'is-danger'}" />
          <span class="icon is-small is-right">
              <i class="fas fa-check" />
            </span>
        </div>
      </div>
      {/if}
    </div>

    <div class="box {showClient ? '' : 'is-paddingless'}">
      <div class="has-icons-left hoverable" on:click={toggleClient}>
        <span class="icon is-right">
          <i class="fas fa-address-card" />
        </span>
        Client
      </div>

      {#if showClient}
        <div class="field">
          <label class="label is-small" for="customer-name">
            Nom du client
          </label>
          <div class="control has-icons-right">
            <input
              id="customer-name"
              type="text"
              on:focus={onFocus}
              on:focusout={onFocusOut}
              bind:value={customer.name}
              placeholder="Customer name of the document"
              class="input is-small {customer.name ? 'is-success' : 'is-danger'}" />
            <span class="icon is-small is-right">
              <i class="fas fa-check" />
            </span>
          </div>
        </div>

      <div class="field">
        <label class="label is-small" for="customer-finalClient">Client Final</label>
        <div class="control has-icons-right">
          <input
                  id="customer-finalClient"
                  type="text"
                  on:focus={onFocus}
                  on:focusout={onFocusOut}
                  bind:value={customer.finalClient}
                  placeholder="Customer finalClient of the document"
                  class="input is-small {customer.finalClient ? 'is-success' : 'is-danger'}" />
          <span class="icon is-small is-right">
              <i class="fas fa-check" />
            </span>
        </div>
      </div>

        <div class="field">
          <label class="label is-small" for="customer-address">Addresse</label>
          <div class="control has-icons-right">
            <input
              id="customer-address"
              type="text"
              on:focus={onFocus}
              on:focusout={onFocusOut}
              bind:value={customer.address}
              placeholder="Customer address of the document"
              class="input is-small {customer.address ? 'is-success' : 'is-danger'}" />
            <span class="icon is-small is-right">
              <i class="fas fa-check" />
            </span>
          </div>
        </div>

        <div class="field">
          <label class="label is-small" for="customer-cp">Code Postale</label>
          <div class="control has-icons-right">
            <input
              id="customer-cp"
              type="text"
              on:focus={onFocus}
              on:focusout={onFocusOut}
              bind:value={customer.cp}
              placeholder="Customer cp of the document"
              class="input is-small {customer.cp ? 'is-success' : 'is-danger'}" />
            <span class="icon is-small is-right">
              <i class="fas fa-check" />
            </span>
          </div>
        </div>

      <div class="field">
        <label class="label is-small" for="customer-commandNumber">N° de Commande</label>
        <div class="control has-icons-right">
          <input
                  id="customer-commandNumber"
                  type="text"
                  on:focus={onFocus}
                  on:focusout={onFocusOut}
                  bind:value={customer.commandNumber}
                  placeholder="Customer commandNumber of the document"
                  class="input is-small {customer.commandNumber ? 'is-success' : 'is-danger'}" />
          <span class="icon is-small is-right">
              <i class="fas fa-check" />
            </span>
        </div>
      </div>

      <div class="field">
        <label class="label is-small" for="customer-affaireNumber">N° d'affaire</label>
        <div class="control has-icons-right">
          <input
                  id="customer-affaireNumber"
                  type="text"
                  on:focus={onFocus}
                  on:focusout={onFocusOut}
                  bind:value={customer.affaireNumber}
                  placeholder="Customer affaireNumber of the document"
                  class="input is-small {customer.affaireNumber ? 'is-success' : 'is-danger'}" />
          <span class="icon is-small is-right">
              <i class="fas fa-check" />
            </span>
        </div>
      </div>
      {/if}
    </div>

    <div class="field is-grouped">
      <div class="control">
        <button
          id="save-button"
          on:click={saveInformations}
          class="button is-info">
          Save informations locally
        </button>
      </div>
      <div class="control">
        <button
          id="print-button"
          on:click={printDocument}
          class="button is-primary">
          Print
        </button>
      </div>
    </div>
  </div>
{/if}

{#if style == 'jb'}
<Example1
        focused={focused}
        title={title}
        myCompany={myCompany}
        customer={customer}
        date_simple_fr={date_simple_fr}
        date_full_fr={date_full_fr}
        year={year}
        quantity={quantity}
        price_without_vat={price_without_vat_value}
        vat={vat}
        date_simple_fr_60_days={date_simple_fr_60_days}
        total_without_vat={total_without_vat}
        price_of_vat={price_of_vat}
        total_with_vat={total_with_vat}
        start_date_facturation={start_date_facturation}
        end_date_facturation={end_date_facturation}
        designation={designation}
/>
{/if}

{#if style == 'henri'}
<Example2
        focused={focused}
        title={title}
        myCompany={myCompany}
        customer={customer}
        date_simple_fr={date_simple_fr}
        quantity={quantity}
        price_without_vat={price_without_vat_value}
        vat={vat}
        total_without_vat={total_without_vat}
        price_of_vat={price_of_vat}
        total_with_vat={total_with_vat}
        designation={designation}
        start_date_facturation={start_date_facturation}
        end_date_facturation={end_date_facturation}
/>
{/if}