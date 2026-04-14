name: build-sherpa-onnx-wasm-kws

on:
  workflow_dispatch:
  push:
    branches:
      - main
      - master

jobs:
  build-kws-wasm:
    runs-on: ubuntu-22.04

    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          submodules: recursive

      - name: Install dependencies
        run: |
          sudo apt-get update
          sudo apt-get install -y \
            git \
            cmake \
            ninja-build \
            python3 \
            python3-pip \
            curl \
            wget \
            tar

      - name: Setup emsdk 3.1.53
        shell: bash
        run: |
          git clone https://github.com/emscripten-core/emsdk.git
          cd emsdk
          ./emsdk install 3.1.53
          ./emsdk activate 3.1.53

      - name: Show emsdk version
        shell: bash
        run: |
          source emsdk/emsdk_env.sh
          emcc -v

      - name: Build sherpa-onnx KWS wasm
        shell: bash
        run: |
          source emsdk/emsdk_env.sh
          chmod +x ./build-wasm-simd-kws.sh
          ./build-wasm-simd-kws.sh

      - name: Upload artifacts
        uses: actions/upload-artifact@v4
        with:
          name: sherpa-onnx-wasm-kws
          path: build-wasm-simd-kws/install/bin/wasm/
