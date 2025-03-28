import { useEffect, useRef, useState } from "react";

// Sound effects (add your own paths)
const jumpSound = new Audio('/sounds/jump.mp3');
const collectSound = new Audio('/sounds/collect.mp3');
const hitSound = new Audio('/sounds/hit.mp3');

export default function JunglePlatformer() {
  const canvasRef = useRef(null);
  const [score, setScore] = useState(0);
  const [gameOver, setGameOver] = useState(false);
  const [powerUpActive, setPowerUpActive] = useState(false);

  useEffect(() => {
    const canvas = canvasRef.current;
    const ctx = canvas.getContext("2d");
    let animationFrameId;

    // Game assets
    const monkey = { x: 50, y: 200, width: 40, height: 40, dy: 0, jump: -8, gravity: 0.5 };
    const bananas = [{ x: 300, y: 220, width: 20, height: 20 }];
    const enemies = [{ x: 500, y: 230, width: 30, height: 30 }];
    const powerUps = [{ x: 700, y: 200, width: 30, height: 30 }];
    const platforms = [
      { x: 100, y: 300, width: 100, height: 10, dx: 1 },
      { x: 400, y: 250, width: 100, height: 10, dx: -1 },
    ];

    function playSound(sound) {
      sound.play();
    }

    function drawMonkey() {
      ctx.fillStyle = powerUpActive ? "gold" : "brown";
      ctx.fillRect(monkey.x, monkey.y, monkey.width, monkey.height);
