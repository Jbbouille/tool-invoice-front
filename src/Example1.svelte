<script>
  export let title;
  export let myCompany;
  export let customer;
  export let date_simple_fr;
  export let date_full_fr;
  export let year;
  export let quantity;
  export let price_without_vat;
  export let vat;
  export let date_simple_fr_60_days;
  export let total_without_vat;
  export let price_of_vat;
  export let total_with_vat;
  export let designation;
  export let start_date_facturation
  export let end_date_facturation
  export let focused;
</script>

<style>
    table, td, th {
        border: 1px solid #eceff1;
        text-align: left;
    }

    table {
        border-collapse: collapse;
        width: 100%;
    }

    th, td {
        padding: 9px;
    }

    th {
        background-color: #eceff1;
    }

    .invoice {
        display: grid;
        grid-template-columns: 26% auto 29% 32% 14%;
        grid-template-rows: 7% 19% 7% 0 auto 9% 18% 15% 0;

        font-family: Arial, Helvetica, sans-serif;
    }

    .title {
        grid-column-start: 5;
        grid-column-end: 5;
        grid-row-start: 1;
        grid-row-end: 1;
        justify-self: end;

        font-size: 24px;
        font-weight: bold;
    }

    .my-company {
        display: flex;
        flex-direction: column;
        justify-content: space-evenly;

        grid-column-start: 1;
        grid-column-end: 4;
        grid-row-start: 1;
        grid-row-end: 3;
    }

    .my-company-group-big {
        display: flex;
        flex-direction: column;
        font-size: 15px;
    }

    .my-company-group-small {
        display: flex;
        flex-direction: column;
        font-size: 12px;
    }

    .customer {
        display: flex;
        flex-direction: column;
        justify-content: space-around;

        grid-column-start: end;
        grid-column-end: 4;
        grid-row-start: 2;
        grid-row-end: 2;
    }

    .customer-group {
        display: flex;
        flex-direction: column;

        font-size: 16px;
        text-align: right;
    }

    .name {
        display: flex;
        flex-direction: column;

        grid-column-start: 1;
        grid-column-end: end;
        grid-row-start: 3;
        grid-row-end: 3;
    }

    .name > span:nth-child(1) {
        font-size: 20px;
        font-weight: bold;
    }

    .goods {
        grid-column-start: 1;
        grid-column-end: end;
        grid-row-start: 5;
        grid-row-end: 5;
    }

    .table-goods {
        font-size: 9px;
        text-align: left;
        width: 100%;
    }

    .condition {
        width: 175px;

        grid-column-start: 1;
        grid-column-end: 1;
        grid-row-start: 6;
        grid-row-end: 6;

        text-align: justify;
        font-size: 15px;
    }

    .total {
        display: flex;
        flex-direction: column;
        justify-content: space-around;

        grid-column-start: 4;
        grid-column-end: end;
        grid-row-start: 6;
        grid-row-end: 6;

        border-style: solid;
        border-width: 1px;
        border-color: gainsboro;
        background-color: aliceblue;

        padding: 10px 10px 10px 10px;
    }

    .total > div {
        display: flex;
        justify-content: space-between;
    }

    .footer {
        grid-column-start: 1;
        grid-column-end: end;
        grid-row-start: 8;
        grid-row-end: 8;
        font-size: 9px;
        text-align: justify;
    }

    .numberOfPages {
        grid-column-start: 5;
        grid-column-end: end;
        grid-row-start: 9;
        grid-row-end: 9;
    }

    .command {
        grid-column-start: 4;
        grid-column-end: end;
        grid-row-start: 3;
        grid-row-end: 3;
        display: flex;
        flex-direction: column;
    }

    .payement {
        grid-column-start: 1;
        grid-column-end: 4;
        grid-row-start: 7;
        grid-row-end: 7;
        display: flex;
        flex-direction: column;
        justify-content: center;
    }

    .payement-group {
        border-style: solid;
        border-width: 1px;
        border-color: gainsboro;
    }

    .payement-group > div {
        display: flex;
        justify-content: space-between;
        align-items: flex-start;
    }
</style>

<div class="invoice sheet padding-10mm">
    <div class="title {focused === 'title' ? 'is-focused' : ''}">{title}</div>
    <div class="my-company">
        <div class="my-company-group-big">
            <span><span class="{focused === 'myCompany-name' ? 'is-focused' : ''}">{myCompany.name}</span></span>
            <span><span class="{focused === 'myCompany-declaraction' ? 'is-focused' : ''}">{myCompany.declaraction}</span></span>
            <span><span class="{focused === 'myCompany-siret' ? 'is-focused' : ''}">{myCompany.siret}</span> au <span class="{focused === 'myCompany-registration' ? 'is-focused' : ''}">{myCompany.registration}</span></span>
            <span></span>
            <span><span class="{focused === 'myCompany-address' ? 'is-focused' : ''}">{myCompany.address}</span></span>
            <span><span class="{focused === 'myCompany-cp' ? 'is-focused' : ''}">{myCompany.cp}</span></span>
        </div>
        <div class="my-company-group-small">
            <span><span class="{focused === 'myCompany-tel' ? 'is-focused' : ''}">{myCompany.tel}</span></span>
            <span><span class="{focused === 'myCompany-email' ? 'is-focused' : ''}">{myCompany.email}</span></span>
        </div>
    </div>
    <div class="customer">
        <div class="customer-group">
            <span><span class="{focused === 'customer-name' ? 'is-focused' : ''}">{customer.name}</span></span>
            <span><span class="{focused === 'customer-address' ? 'is-focused' : ''}">{customer.address}</span></span>
            <span><span class="{focused === 'customer-cp' ? 'is-focused' : ''}">{customer.cp}</span></span>
        </div>
        <div class="customer-group">
            <span>N° Commande : <span class="{focused === 'customer-commandNumber' ? 'is-focused' : ''}">{customer.commandNumber}</span></span>
            <span>N° Affaire : <span class="{focused === 'customer-affaireNumber' ? 'is-focused' : ''}">{customer.affaireNumber}</span></span>
            <span>Client final : <span class="{focused === 'customer-finalClient' ? 'is-focused' : ''}">{customer.finalClient}</span></span>
        </div>
    </div>
    <div class="name">
        <span>Facture N° <span class="{focused === 'date_simple_fr' ? 'is-focused' : ''}">{date_simple_fr}</span></span>
        <span>Le <span class="{focused === 'date_simple_fr' ? 'is-focused' : ''}">{date_full_fr}</span>.</span>
    </div>
    <div class="goods">
        <table class="table-goods">
            <thead>
            <tr>
                <th>Référence</th>
                <th>Désignation</th>
                <th>Quantité</th>
                <th>PU Vente</th>
                <th>TVA</th>
                <th>Montant HT</th>
            </tr>
            </thead>
            <tbody>
            <tr>
                <td>ref-00001</td>
                <td ><span class="{focused === 'designation' ? 'is-focused' : ''}">{designation}</span> du <span class="{focused === 'start_date_facturation' ? 'is-focused' : ''}">{start_date_facturation}</span> au <span class="{focused === 'end_date_facturation' ? 'is-focused' : ''}">{end_date_facturation}</span> <span>{year}</span>.</td>
                <td class="{focused === 'quantity' ? 'is-focused' : ''}">{quantity}</td>
                <td class="{focused === 'price_without_vat' ? 'is-focused' : ''}">{price_without_vat}</td>
                <td class="{focused === 'vat' ? 'is-focused' : ''}">{vat} %</td>
                <td class="{focused === 'total_without_vat' ? 'is-focused' : ''}">{total_without_vat}</td>
            </tr>
            </tbody>
        </table>
    </div>
    <div class="condition {focused === 'date_simple_fr_60_days' ? 'is-focused' : ''}">
        Conditions de paiement : {total_with_vat} à payer le {date_simple_fr_60_days}
        (60 jours) par virement.
    </div>
    <div class="total">
        <div>
            <span>Total HT</span>
            <span class="{focused === 'total_without_vat' ? 'is-focused' : ''}">{total_without_vat}</span>
        </div>
        <div>
            <span>TVA ( {vat} % )</span>
            <span class="{focused === 'price_of_vat' ? 'is-focused' : ''}">{price_of_vat}</span>
        </div>
        <div>
            <span>Total TTC</span>
            <span class="{focused === 'total_with_vat' ? 'is-focused' : ''}">{total_with_vat}</span>
        </div>
    </div>
    <div class="payement">
        <div class="payement-group">
            <div>
                <span>Référence IBAN :</span>
                <span class="{focused === 'myCompany-iban' ? 'is-focused' : ''}">{myCompany.iban}</span>
            </div>
            <div>
                <span>SWIFT :</span>
                <span class="{focused === 'myCompany-swift' ? 'is-focused' : ''}">{myCompany.swift}</span>
            </div>
        </div>
    </div>
    <div class="footer">
        <p>
            CLAUSE DE RÉSERVE DE PROPRIÉTÉ : Conformément à la loi 80.335 du 12 mai
            1980, nous réservons la propriété des produits et marchandises, objets des
            présents débits, jusqu'au paiement de l'intégralité du prix et de ses
            accessoires. En cas de non paiement total ou partiel du prix de l'échéance
            pour quelque cause que ce soit, de convention expresse, nous nous
            réservons la faculté, sans formalités, de reprendre matériellement
            possession de ces produits ou marchandises à vos frais, risques et périls.
            Pénalité de retard : 3 fois le taux d'intérêt légal après date échéance.
            Escompte pour règlement anticipé : 0% (sauf condition particulière définie
            dans les conditions de règlement) Le montant de l'indemnité forfaitaire
            pour frais de recouvrement prévue en douzième alinéa de l'article L441-6
            est fixé à 40 Euros en matière commerciale.
        </p>
    </div>
    <div class="numberOfPages">Page 1/1</div>
</div>
