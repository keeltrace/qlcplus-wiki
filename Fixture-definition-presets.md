# Presets in fixture definitions

In [fixture definitions](https://github.com/mcallegari/qlcplus/tree/master/resources/fixtures), `<Channel>` and `<Capability>` elements can have a `Preset` attribute which specifies the type of the channel / capability to help QLC+ adapt e.g. the 3D Preview to the properties and peculiarities of each fixture.

See [`qlcchannel.h`](https://github.com/mcallegari/qlcplus/blob/master/engine/src/qlcchannel.h#L97) and [`qlccapability.h`](https://github.com/mcallegari/qlcplus/blob/master/engine/src/qlccapability.h#L101) for a list of available presets and just search the repository for the name of a preset to see how and where it is used.

Capability presets can have parameters (*resources*), which are specified using the `Res1` and `Res2` attributes on the `<Capability>` element. The purpose and type is dependent on the preset, so look at other usages of the preset and at the `presetType` and `presetUnits` functions of [`qlccapability.cpp`](https://github.com/mcallegari/qlcplus/blob/master/engine/src/qlccapability.cpp).

When adding / updating / removing a **channel preset**, do so in all of the following places:

* [Fixture definition XSD schema](https://github.com/mcallegari/qlcplus/blob/master/resources/schemas/fixture.xsd#L149)
* [Fixtures tool](https://github.com/mcallegari/qlcplus/blob/master/resources/fixtures/scripts/fixtures-tool.py)
* [`qlcchannel.h`](https://github.com/mcallegari/qlcplus/blob/master/engine/src/qlcchannel.h#L97)
* [`qlcchannel.cpp`](https://github.com/mcallegari/qlcplus/blob/master/engine/src/qlcchannel.cpp), both the `setPreset` and `addPresetCapability` functions
* All the places where it is used, i.e. fixtures and code; just search the repository for the preset name.

When adding / updating / removing a **capability preset**, do so in all of the following places:

* [Fixture definition XSD schema](https://github.com/mcallegari/qlcplus/blob/master/resources/schemas/fixture.xsd#L224)
* [`qlccapability.h`](https://github.com/mcallegari/qlcplus/blob/master/engine/src/qlccapability.h#L101)
* [`qlccapability.cpp`](https://github.com/mcallegari/qlcplus/blob/master/engine/src/qlccapability.cpp), both the `presetType` and `presetUnits` functions (if the preset uses resources)
* All the places where it is used, i.e. fixtures and code; just search the repository for the preset name.

In both cases, you might want to open an issue at the [Open Fixture Library repository](https://github.com/OpenLightingProject/open-fixture-library) to notify them about changes of the fixture definition format, so that the QLC+ export there can be adjusted.