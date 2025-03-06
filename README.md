# MealPlannerWebsite
A meal planner website
import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Select, SelectItem } from "@/components/ui/select";
import { motion } from "framer-motion";

const mealPlans = [
  { name: "Vegetarian", description: "Plant-based meals with balanced nutrition." },
  { name: "Keto", description: "Low-carb, high-fat meals for ketosis." },
  { name: "Mediterranean", description: "Fresh vegetables, olive oil, and lean protein." },
];

const dishes = [
  { name: "Grilled Salmon", calories: 400, diet: "Mediterranean" },
  { name: "Avocado Salad", calories: 250, diet: "Vegetarian" },
  { name: "Keto Omelet", calories: 300, diet: "Keto" },
];

export default function MealPlanner() {
  const [selectedDiet, setSelectedDiet] = useState("All");
  const [search, setSearch] = useState("");

  const filteredDishes = dishes.filter(
    (dish) =>
      (selectedDiet === "All" || dish.diet === selectedDiet) &&
      dish.name.toLowerCase().includes(search.toLowerCase())
  );

  return (
    <div className="p-6 space-y-6">
      <motion.h1 className="text-3xl font-bold" initial={{ opacity: 0 }} animate={{ opacity: 1 }}>
        Interactive Meal Planner
      </motion.h1>
      
      <div className="grid grid-cols-1 md:grid-cols-3 gap-4">
        {mealPlans.map((plan, index) => (
          <Card key={index} className="p-4">
            <CardContent>
              <h2 className="text-xl font-semibold">{plan.name}</h2>
              <p className="text-gray-600">{plan.description}</p>
            </CardContent>
          </Card>
        ))}
      </div>
      
      <div className="flex gap-4">
        <Input
          placeholder="Search dishes..."
          value={search}
          onChange={(e) => setSearch(e.target.value)}
        />
        <Select value={selectedDiet} onValueChange={setSelectedDiet}>
          <SelectItem value="All">All Diets</SelectItem>
          {mealPlans.map((plan) => (
            <SelectItem key={plan.name} value={plan.name}>{plan.name}</SelectItem>
          ))}
        </Select>
      </div>
      
      <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
        {filteredDishes.map((dish, index) => (
          <Card key={index} className="p-4">
            <CardContent>
              <h3 className="text-lg font-semibold">{dish.name}</h3>
              <p className="text-gray-500">Calories: {dish.calories}</p>
              <p className="text-sm text-gray-400">Diet: {dish.diet}</p>
            </CardContent>
          </Card>
        ))}
      </div>
    </div>
  );
}
