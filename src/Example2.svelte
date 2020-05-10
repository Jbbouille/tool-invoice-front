<script>
  export let title;
  export let myCompany;
  export let customer;
  export let date_simple_fr;
  export let quantity;
  export let price_without_vat;
  export let vat;
  export let total_without_vat;
  export let price_of_vat;
  export let total_with_vat;
  export let designation;
  export let start_date_facturation;
  export let end_date_facturation;
  export let focused;
</script>

<style>
    .invoice {
        display: flex;
        flex-direction: column;
    }
    .title {
        align-self: center;
        border-bottom: 1px solid;
        width: 800px;
        text-align: center;
        padding-bottom: 25px;
    }
    .customer {
        display: flex;
        flex-direction: column;
    }
    .customer > span {
        text-align: right;
    }
    .information {
        width: 350px;
        border: 1px solid black;
    }
    table, th, tr, td {
        border: 1px solid black;
    }
    td, th {
        padding: 3px;
    }
    th {
        background-color: #AED581;
    }
    td {
        background-color: #F1F8E9;
    }
    .description {
        padding-top: 65px;
    }
    .description > table > thead > tr > th:nth-child(1) {
        width: 250px;
    }
    .total {
        padding-top: 90px;
        padding-left: 365px;
    }
    .payement {
        padding-top: 100px;
    }
    .company {
        padding-top: 40px;
        display: flex;
        flex-direction: column;
        text-align: center;
    }
</style>

<div class="invoice sheet padding-25mm">
    <div class="title">
        Facture
    </div>
    <div class="customer">
        <span><span class="{focused === 'customer-name' ? 'is-focused' : ''}">{customer.name}</span></span>
        <span><span class="{focused === 'customer-finalClient' ? 'is-focused' : ''}">{customer.finalClient}</span></span>
        <span><span class="{focused === 'customer-address' ? 'is-focused' : ''}">{customer.address}</span></span>
        <span><span class="{focused === 'customer-cp' ? 'is-focused' : ''}">{customer.cp}</span></span>
    </div>

    <table class="information">
        <tr>
            <td style="background-color: #C5E1A5">Facture</td>
            <td class="{focused === 'title' ? 'is-focused' : ''}" style="background-color: #C5E1A5">{title}</td>
        </tr>
        <tr>
            <td>Date émission</td>
            <td class="{focused === 'date_simple_fr' ? 'is-focused' : ''}">{date_simple_fr}</td>
        </tr>
        <tr>
            <td>Votre contact</td>
            <td class="{focused === 'myCompany-contact' ? 'is-focused' : ''}">{myCompany.contact}</td>
        </tr>
        <tr>
            <td>Période de facturation</td>
            <td><span class="{focused === 'start_date_facturation' ? 'is-focused' : ''}">{start_date_facturation}</span> – <span class="{focused === 'end_date_facturation' ? 'is-focused' : ''}">{end_date_facturation}</span></td>
        </tr>
    </table>

    <div class="description">
        <table>
            <thead>
                <tr>
                    <th>Descriptif</th>
                    <th>Quantité</th>
                    <th>Prix unitaire H.T.</th>
                    <th>Total H.T.</th>
                    <th>TVA</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td class="{focused === 'designation' ? 'is-focused' : ''}">{designation}</td>
                    <td class="{focused === 'quantity' ? 'is-focused' : ''}">{quantity}</td>
                    <td class="{focused === 'price_without_vat' ? 'is-focused' : ''}">{price_without_vat}</td>
                    <td class="{focused === 'total_without_vat' ? 'is-focused' : ''}">{total_without_vat}</td>
                    <td class="{focused === 'vat' ? 'is-focused' : ''}">{vat}%</td>
                </tr>
            </tbody>
        </table>
    </div>

    <div class="total">
        <table>
            <tr>
                <td>Total H.T.</td>
                <td class="{focused === 'total_without_vat' ? 'is-focused' : ''}">{total_without_vat}</td>
                <td></td>
            </tr>
            <tr>
                <td>T.V.A.</td>
                <td class="{focused === 'price_of_vat' ? 'is-focused' : ''}">{price_of_vat}</td>
                <td class="{focused === 'vat' ? 'is-focused' : ''}">{vat} %</td>
            </tr>
            <tr>
                <td style="background-color: #C5E1A5">Total T.T.C.</td>
                <td style="background-color: #C5E1A5" class="{focused === 'total_with_vat' ? 'is-focused' : ''}">{total_with_vat}</td>
                <td style="background-color: #C5E1A5"></td>
            </tr>
        </table>
    </div>

    <div class="payement">
        <div>
            <span>Conditions de paiement :</span>
            <span>30 jours date d’émission de facture</span>
        </div>
        <div>
            <span>Référence IBAN :</span>
            <span class="{focused === 'myCompany-iban' ? 'is-focused' : ''}">{myCompany.iban}</span>
        </div>
        <div>
            <span>SWIFT :</span>
            <span class="{focused === 'myCompany-swift' ? 'is-focused' : ''}">{myCompany.swift}</span>
        </div>
    </div>

    <div class="company">
        <span><span class="{focused === 'myCompany-name' ? 'is-focused' : ''}">{myCompany.name}</span></span>
        <span><span class="{focused === 'myCompany-address' ? 'is-focused' : ''}">{myCompany.address}</span></span>
        <span><span class="{focused === 'myCompany-cp' ? 'is-focused' : ''}">{myCompany.cp}</span></span>
        <span><span class="{focused === 'myCompany-email' ? 'is-focused' : ''}">{myCompany.email}</span></span>
        <span><span class="{focused === 'myCompany-siret' ? 'is-focused' : ''}">{myCompany.siret}</span></span>
    </div>
</div>