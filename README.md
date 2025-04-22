import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { motion } from "framer-motion";

const words = [
  {
    word: "يقرأ",
    image: "https://example.com/read.png",
    audio: "https://example.com/read.mp3",
  },
  {
    word: "يلعب",
    image: "https://example.com/play.png",
    audio: "https://example.com/play.mp3",
  },
  {
    word: "يأكل",
    image: "https://example.com/eat.png",
    audio: "https://example.com/eat.mp3",
  },
  {
    word: "شرب",
    image: "https://example.com/drink.png",
    audio: "https://example.com/drink.mp3",
  },
  {
    word: "كتب",
    image: "https://example.com/write.png",
    audio: "https://example.com/write.mp3",
  },
];

export default function Game() {
  const [selected, setSelected] = useState(null);

  const playAudio = (src) => {
    const audio = new Audio(src);
    audio.play();
  };

  const handleSelect = (item) => {
    setSelected(item);
    playAudio(item.audio);
  };

  return (
    <div className="min-h-screen bg-orange-50 flex flex-col items-center justify-center p-4">
      <h1 className="text-4xl font-bold mb-6">لعبة تعلم الأفعال</h1>

      <div className="grid grid-cols-2 gap-4 mb-8">
        {words.map((item, index) => (
          <Button
            key={index}
            className="text-2xl p-5 rounded-2xl shadow-md hover:bg-orange-100"
            onClick={() => handleSelect(item)}
          >
            {item.word}
          </Button>
        ))}
      </div>

      {selected && (
        <motion.div
          className="w-full max-w-sm"
          initial={{ opacity: 0, scale: 0.8 }}
          animate={{ opacity: 1, scale: 1 }}
        >
          <Card className="text-center bg-white rounded-2xl shadow-lg p-4">
            <CardContent>
              <img src={selected.image} alt={selected.word} className="w-48 h-48 mx-auto mb-4" />
              <p className="text-3xl font-semibold">{selected.word}</p>
            </CardContent>
          </Card>
        </motion.div>
      )}
    </div>
  );
