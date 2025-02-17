#wonderla-rides
import React, { useState, useEffect } from "react";
import { motion } from "framer-motion";
import RideCard from "./RideCard";
import CategorySidebar from "./CategorySidebar";
import CarouselControls from "./CarouselControls";
import rideData from "./rideData.json";

const RidesSection = () => {
  const [category, setCategory] = useState("All");
  const [rides, setRides] = useState(rideData);
  const [currentIndex, setCurrentIndex] = useState(0);

  useEffect(() => {
    if (category === "All") {
      setRides(rideData);
    } else {
      setRides(rideData.filter((ride) => ride.category === category));
    }
  }, [category]);

  const nextSlide = () => {
    setCurrentIndex((prev) => (prev + 1) % rides.length);
  };

  const prevSlide = () => {
    setCurrentIndex((prev) => (prev - 1 + rides.length) % rides.length);
  };

  return (
    <div className="flex space-x-4 p-6">
      <CategorySidebar setCategory={setCategory} />
      <div className="relative w-full overflow-hidden">
        <motion.div
          className="flex"
          animate={{ x: `-${currentIndex * 100}%` }}
          transition={{ ease: "easeInOut", duration: 0.5 }}
        >
          {rides.map((ride, index) => (
            <RideCard key={index} ride={ride} />
          ))}
        </motion.div>
        <CarouselControls next={nextSlide} prev={prevSlide} />
      </div>
    </div>
  );
};

export default RidesSection;
