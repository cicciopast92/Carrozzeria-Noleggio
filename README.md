import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Tabs, TabsList, TabsTrigger, TabsContent } from "@/components/ui/tabs";

export default function F&LApp() {
  const [search, setSearch] = useState("");
  const [rentals, setRentals] = useState([
    { id: 1, name: "Fiat Panda", available: true },
   
  ]);

  return (
    <div className="p-6 max-w-4xl mx-auto">
      <h1 className="text-2xl font-bold mb-4">Carrozzeria & Noleggio Auto</h1>
      <Tabs defaultValue="repair">
        <TabsList className="mb-4">
          <TabsTrigger value="repair">Riparazioni</TabsTrigger>
          <TabsTrigger value="rental">Noleggio</TabsTrigger>
        </TabsList>
        
        <TabsContent value="repair">
          <Card>
            <CardContent className="p-4">
              <h2 className="text-xl font-semibold mb-2">Prenota una Riparazione</h2>
              <Input placeholder="Descrivi il problema..." className="mb-2" />
              <Button>Prenota</Button>
            </CardContent>
          </Card>
        </TabsContent>

        <TabsContent value="rental">
          <Card>
            <CardContent className="p-4">
              <h2 className="text-xl font-semibold mb-2">Auto Disponibili</h2>
              <Input
                placeholder="Cerca auto..."
                value={search}
                onChange={(e) => setSearch(e.target.value)}
                className="mb-2"
              />
              <div className="space-y-2">
                {rentals
                  .filter((car) => car.name.toLowerCase().includes(search.toLowerCase()))
                  .map((car) => (
                    <Card key={car.id} className="p-3 flex justify-between items-center">
                      <span>{car.name}</span>
                      <Button disabled={!car.available}>
                        {car.available ? "Noleggia" : "Non disponibile"}
                      </Button>
                    </Card>
                  ))}
              </div>
            </CardContent>
          </Card>
        </TabsContent>
      </Tabs>
    </div>
  );
}
