<template>
  <div class="min-h-screen bg-gray-50 p-4 md:p-8">
    <div class="mx-auto max-w-4xl">
      <div class="bg-white shadow-lg rounded-lg border-0">
        <div class="p-8 md:p-12">
          <!-- Header Section -->
          <div
            class="flex flex-col md:flex-row justify-between items-start mb-12"
          >
            <!-- Company Logo and Name -->
            <div class="flex items-center gap-3 mb-6 md:mb-0">
              <div
                class="w-8 h-8 bg-indigo-600 rounded-lg flex items-center justify-center"
              >
                <img
                  class="w-full h-full object-cover rounded"
                  :src="logoUrl"
                  alt="Logo"
                />
              </div>
              <div>
                <h2 class="text-lg font-semibold text-gray-900">
                  {{ invoice.seller.name }}
                </h2>
              </div>
            </div>

            <!-- Invoice Details -->
            <div class="text-right">
              <h1 class="text-3xl font-bold text-indigo-600 mb-4">FACTURA</h1>
              <div class="space-y-1">
                <p class="text-sm text-gray-500">
                  Date:
                  <span class="text-gray-700">{{ invoice.invoice.date }}</span>
                </p>
                <p class="text-sm text-gray-500">
                  Invoice #:
                  <span class="text-gray-700">{{
                    invoice.invoice.number
                  }}</span>
                </p>
              </div>
            </div>
          </div>

          <div class="border-t border-gray-200 mb-8"></div>

          <!-- Bill To Section -->
          <div class="mb-8">
            <h3 class="text-lg font-semibold text-indigo-600 mb-4">Bill To:</h3>
            <div class="bg-gray-50 rounded-lg p-4">
              <p class="font-medium text-gray-900">{{ invoice.buyer.name }}</p>
              <p class="text-gray-600">{{ invoice.buyer.address }}</p>
              <p class="text-gray-600">
                {{ invoice.buyer.town }}, {{ invoice.buyer.province }}
                {{ invoice.buyer.postal_code }}
              </p>
            </div>
          </div>

          <!-- Items Table -->
          <div class="mb-8">
            <div class="overflow-x-auto">
              <table
                class="w-full border border-gray-200 rounded-lg overflow-hidden"
              >
                <thead>
                  <tr class="bg-indigo-50 border-b border-indigo-100">
                    <th
                      class="text-left py-4 px-6 font-semibold text-indigo-700"
                    >
                      DESCRIPTION
                    </th>
                    <th
                      class="text-center py-4 px-6 font-semibold text-indigo-700"
                    >
                      QUANTITY
                    </th>
                    <th
                      class="text-right py-4 px-6 font-semibold text-indigo-700"
                    >
                      PRICE
                    </th>
                  </tr>
                </thead>
                <tbody>
                  <tr
                    v-for="(item, index) in invoice.products"
                    :key="index"
                    :class="[
                      'border-b border-gray-100 hover:bg-gray-50 transition-colors',
                      index % 2 === 0 ? 'bg-white' : 'bg-gray-50/30',
                    ]"
                  >
                    <td class="py-4 px-6 text-gray-900">{{ item.product }}</td>
                    <td class="py-4 px-6 text-center text-gray-700">
                      {{ item.quantity }}
                    </td>
                    <td class="py-4 px-6 text-right text-gray-700">
                      {{ formatCurrency(item.price) }}
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>

          <!-- Totals Section -->
          <div class="flex justify-end">
            <div class="w-full md:w-80">
              <div class="bg-gray-50 rounded-lg p-6 space-y-3">
                <div class="flex justify-between items-center">
                  <span class="text-gray-600">Subtotal:</span>
                  <span class="font-medium text-gray-900">
                    {{ formatCurrency(invoice.invoice.priceWithoutTax) }}
                  </span>
                </div>

                <div class="flex justify-between items-center">
                  <span class="text-gray-600">Tax Rate:</span>
                  <span class="text-gray-700">
                    {{ formatCurrency(invoice.invoice.taxPrice) }}
                    ({{ invoice.invoice.taxRate }}%)
                  </span>
                </div>

                <div class="border-t border-gray-200 my-3"></div>

                <div class="flex justify-between items-center">
                  <span class="text-lg font-semibold text-gray-900"
                    >Total:</span
                  >
                  <span class="text-2xl font-bold text-indigo-600">
                    {{ formatCurrency(invoice.invoice.total) }}
                  </span>
                </div>
              </div>
            </div>
          </div>
          <!-- Footer -->
          <div class="mt-12 pt-8 border-t border-gray-200">
            <div class="text-center">
              <p class="text-sm text-gray-500 font-medium tracking-wider">
                PAY-ME
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from "vue";

const props = defineProps({
  invoice: {
    required: true,
    type: Object,
  },
});

const logoUrl = "";

const formatCurrency = (amount) => {
  return new Intl.NumberFormat("es-ES", {
    style: "currency",
    currency: "EUR",
    minimumFractionDigits: 2,
  }).format(amount);
};
</script>
