<template>
  <tr>
    <slot></slot>
    <td class="font-monospace">{{ station.id }}</td>
    <th>
      <a :href="data(station)">{{ station.name }}</a>
    </th>
    <td>{{ station.state }}</td>
    <td class="text-end">{{ station.altitude }}&thinsp;m&thinsp;ü.A.</td>
    <td><a :href="osm(station)">osm</a> <a :href="geo(station)">geo:</a></td>
    <td class="font-monospace">
      {{ station.valid_from.slice(0, "2006-01-02".length) }}
    </td>
    <td class="font-monospace">
      {{ station.valid_to.slice(0, "2006-01-02".length) }}
    </td>
  </tr>
</template>

<script setup lang="ts">
import type { StationMetadata } from "./openapi";

defineProps<{
  station: StationMetadata;
}>();

function data(station: StationMetadata) {
  return `/station/?station=${station.id}&parameter=TL&parameter=RR`;
}
function geo(station: StationMetadata) {
  return `geo:${station.lon},${station.lat},${station.altitude}`;
}
function osm(station: StationMetadata) {
  return `https://www.openstreetmap.org/?mlat=${station.lat}&mlon=${station.lon}`;
}
</script>
