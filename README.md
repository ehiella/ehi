# ehi
import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";

export default function QuoteCreator() {
  const [quote, setQuote] = useState("");
  const [image, setImage] = useState(null);

  const handleImageUpload = (event) => {
    const file = event.target.files[0];
    if (file) {
      const reader = new FileReader();
      reader.onloadend = () => {
        setImage(reader.result);
      };
      reader.readAsDataURL(file);
    }
  };

  return (
    <div className="flex flex-col items-center p-6 bg-gray-100 min-h-screen">
      <Card className="w-full max-w-2xl bg-white p-6 shadow-lg border rounded-lg">
        <CardContent>
          <h1 className="text-2xl font-bold text-center mb-4">Newspaper Quote Creator</h1>
          <textarea
            className="w-full p-2 border rounded-md text-lg"
            placeholder="Enter your quote here..."
            value={quote}
            onChange={(e) => setQuote(e.target.value)}
          />
          <div className="mt-4">
            <input type="file" accept="image/*" onChange={handleImageUpload} className="mb-2" />
            {image && <img src={image} alt="Uploaded" className="w-full h-auto mt-2 rounded-lg border" />}
          </div>
          <div className="flex justify-center mt-4">
            <Button onClick={() => alert("Quote saved!")}>Save Quote</Button>
          </div>
        </CardContent>
      </Card>
    </div>
  );
}
