<template>
  <div id="three-container"></div>
</template>

<script>
import * as THREE from "three";

export default {
  name: "Three",
  data() {
    return {
      camera: null,
      scene: null,
      renderer: null,
      ambLight: null,
      hemisphereLight: null,
      text3D: null,
      pivot: null,
      targetRotation: 0
    };
  },
  methods: {
    init: function() {
      const container = document.getElementById("three-container");
      const canvasWidth = window.innerHeight / 2;
      const canvasHeight = window.innerHeight / 2;

      this.camera = new THREE.PerspectiveCamera(
        65,
        canvasWidth / canvasHeight,
        0.1,
        1000
      );
      this.camera.position.set(0, 0, 6);

      this.scene = new THREE.Scene();

      this.ambLight = new THREE.AmbientLight(0xffffff, 0.6);
      this.scene.add(this.ambLight);

      this.hemisphereLight = new THREE.HemisphereLight(0xffffff, 0x000000, 0.6);
      this.scene.add(this.hemisphereLight);

      // Helper
      const axesHelper = new THREE.AxesHelper(10);
      this.scene.add(axesHelper);
      const gridHelper = new THREE.GridHelper(10, 10);
      this.scene.add(gridHelper);

      this.text3D = this.loadText();
      this.text3D.position.x = -2.6;
      this.text3D.position.y = -1.7;

      this.pivot = new THREE.Object3D().add(this.text3D);
      this.scene.add(this.pivot);

      const cvsClick = document.querySelector("#three-container");

      cvsClick.addEventListener("click", () => {
        this.toggleText();
      });

      this.renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
      this.renderer.setPixelRatio(window.devicePixelRatio);
      this.renderer.setSize(canvasWidth, canvasHeight);
      container.appendChild(this.renderer.domElement);
    },
    animate: function() {
      requestAnimationFrame(this.animate);
      this.pivot.rotation.y -= 0.03;
      this.pivot.rotation.y +=
        (this.targetRotation - this.pivot.rotation.y) * 0.05;
      this.renderer.render(this.scene, this.camera);
    },
    loadText: function() {
      const textLoader = new THREE.FontLoader();
      const objContainer = new THREE.Object3D();
      textLoader.load("/DFPKingGothicGB-Thin-2.json", font => {
        const geometry = new THREE.TextGeometry("皓", {
          font: font,
          size: 3.6,
          height: 0.5
        });
        geometry.computeBoundingBox();
        const geo = new THREE.EdgesGeometry(geometry);
        const lineMaterial = new THREE.LineBasicMaterial({
          color: 0xa27e7e
        });
        const material = new THREE.MeshPhongMaterial({
          color: 0xa6a6a8
        });
        const mesh = new THREE.Mesh(geometry, material);
        const line = new THREE.LineSegments(geo, lineMaterial);
        line.material.depthTest = false;
        line.material.opacity = 1;
        line.material.transparent = true;
        line.visible = false;
        objContainer.add(mesh);
        objContainer.add(line);
      });
      return objContainer;
    },
    toggleText: function() {
      this.text3D.children[0].visible
        ? ((this.text3D.children[0].visible = false),
          (this.text3D.children[1].visible = true))
        : ((this.text3D.children[0].visible = true),
          (this.text3D.children[1].visible = false));
      navigator.vibrate(100);
    }
  },
  mounted() {
    this.init();
    this.animate();
  }
};
</script>

<style scoped>
@media (max-width: 960px) {
  #three-container {
    display: flex;
    justify-content: center;
  }
}
</style>