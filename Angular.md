### Angular Nuances

- **Signals**
  - Computed is read-only
  - Computed signals must be "Pure"
  - This causes ```status = computed(() => this.status.set('Unsaved'););``` -> The Circular Dependency Problem.
  - linkedSignal was specifically designed to replace that messy effect pattern.
  - 
