# nagoya-trip-2025-
/**
 * Project: Nagoya_Vibe_Trip_2025
 * Author: Gemini & User
 * Date: 2025-12-08 to 2025-12-12
 * Description: An immersive 5-day itinerary state machine for Nagoya, Japan.
 */

import { useState, useEffect } from 'react';
import { NagoyaCity, Tokoname, ShirakawaGo, CentralAirport } from './japan/locations';

const NagoyaTripApp = () => {
  // 🌡️ 實時天氣狀態初始化 (基於2025年12月預報)
  const [weather, setWeather] = useState({
    nagoya: { temp: '13°C', condition: '☀️ Sunny/Cloudy', wind: 'Crisp' },
    shirakawa: { temp: '2°C', condition: '❄️ Light Snow', vibe: 'Magical' }
  });

  // 🎒 玩家狀態
  const [playerState, setPlayerState] = useState({
    location: 'TPE_Airport',
    energy: 100,
    inventory: ['Passport', 'Yen', 'Warm Coat', 'Camera'],
    stomach: 'Empty',
    mood: 'Excited'
  });

  // 🗓️ Day 1: The Ceramic Arrival (12/08 Mon)
  const renderDayOne = async () => {
    console.log("--- DAY 1: Landing & Pottery Vibes ---");
    
    // 12:40 PM - Arrival
    await flight.land({ flight: 'SL398', airport: 'NGO', time: '12:40' });
    
    // Mission: Tokoname Exploration
    const tokonameTrip = {
      transit: 'Meitetsu Line (2 stops)',
      lockers: 'Tokoname Station', // Drop luggage here
      spot: 'Pottery Footpath (やきもの散歩道)',
      landmark: 'Tokoname Manekineko (招財貓大道)',
      cafe: {
        name: 'Yamahei Hanare (やまへい はなれ)',
        order: 'Hot Coffee & Afternoon Sweets',
        vibe: 'Renovated Kominka (古民家), Chill, Rustic, Aesthetic',
        note: 'Open until 18:00 on Mondays. Enjoy the warmth of wood.'
      }
    };

    // Evening: Move to Nagoya
    playerState.location = 'Nagoya Station';
    const checkIn = {
      hotel: 'IBIS Styles Nagoya',
      landmark: 'Nana-chan Doll (Check her outfit!)', // 📸 Photo Op
      dinner: 'Izakaya near Meieki or Hotel Relax',
    };
    
    return { ...tokonameTrip, ...checkIn };
  };

  // 🗓️ Day 2: Winter Wonderland (12/09 Tue)
  const renderDayTwo = async () => {
    console.log("--- DAY 2: The Snowy Village ---");
    
    // Weather update: Cold in the mountains
    setWeather({ ...weather, current: weather.shirakawa });

    const busTour = {
      type: 'Day Tour Bus',
      destination: ['Takayama (Old Town)', 'Shirakawa-go (Gassho-zukuri)'],
      food: ['Hida Beef Sushi (飛驒牛壽司)', 'Gohei Mochi'],
      vibe: 'Nostalgic, Snowy, Traditional',
      outfit: 'Heattech + Down Jacket + Waterproof Boots'
    };

    // 🚌 Bus Ride: Watch the scenery change from city to snow
    // 📸 Focus: Three Huts (San-goya) photo spot
    
    playerState.mood = 'Awestruck';
    return busTour;
  };

  // 🗓️ Day 3: History & Curry Craving (12/10 Wed)
  const renderDayThree = async () => {
    console.log("--- DAY 3: Castle, Garden & The Nan Mission ---");
    setWeather({ ...weather, current: weather.nagoya }); // Back to city weather

    const morning = {
      spot: 'Nagoya Castle (名古屋城)',
      highlight: 'Honmaru Goten (Gold paintings)',
    };

    const afternoon = {
      garden: 'Tokugawaen (徳川園)', // Autumn leaves might still linger?
      shopping: 'Osu Shopping District (大須商店街)',
      snack: 'Street Food in Osu (Karaage/Boba)'
    };

    const evening = {
      district: 'Endoji Shopping Street (円頓寺商店街)',
      vibe: 'Showa Retro, Lanterns',
      dinner_mission: {
        target: 'Karisma (カリスマ)', // Assuming Fushimi/Nishiki area near Endoji
        item: 'Cheese Nan or Honey Nan + Curry',
        rating: '⭐⭐⭐⭐⭐',
        description: 'Chewy, massive nan. Spicy rich curry.'
      }
    };

    playerState.stomach = 'Full & Happy';
    return { morning, afternoon, evening };
  };

  // 🗓️ Day 4: Meat & Urban Pulse (12/11 Thu)
  const renderDayFour = async () => {
    console.log("--- DAY 4: Yakiniku & Sakae Style ---");

    const lunch = {
      restaurant: 'Okome to Yakiniku Niku no Yoichi Meieki Honten',
      kanji: 'お米と焼肉 肉のよいち 名駅本店',
      specialty: 'Rice cooked in pot (Kama-meshi) + Yakiniku curtain',
      vibe: 'Sizzling sounds, Aroma of grilled meat'
    };

    const afternoon = {
      area: 'Sakae (栄)',
      activities: ['Shopping (Parco/Lachic)', 'Mirai Tower (Photo)', 'Oasis 21 (Spaceship View)'],
      mission: 'Last minute souvenirs'
    };

    playerState.inventory.push('Don Quijote Bags');
    return { lunch, afternoon };
  };

  // 🗓️ Day 5: Farewell (12/12 Fri)
  const renderDayFive = async () => {
    console.log("--- DAY 5: Departure ---");

    const morning = {
      time: '10:00',
      action: 'Check-out IBIS Nagoya',
      transit: 'uSky / Meitetsu Limited Express -> NGO Airport'
    };

    const airportVibe = {
      location: 'Chubu Centrair International Airport',
      shop: 'Ebi Senbei no Sato (Shrimp Crackers)',
      deck: 'Sky Deck (Watch planes)'
    };

    const departure = {
      flight: 'SL399',
      depart: '13:40',
      destination: 'TPE',
      status: 'On Time'
    };

    return { morning, airportVibe, departure };
  };

  return (
    <div className="trip-container">
      <h1>🇯🇵 Nagoya Vibe Trip 2025</h1>
      <DayOne data={renderDayOne()} />
      <DayTwo data={renderDayTwo()} />
      <DayThree data={renderDayThree()} />
      <DayFour data={renderDayFour()} />
      <DayFive data={renderDayFive()} />
      <Footer msg="Trip Complete. Uploading memories to cloud..." />
    </div>
  );
};

export default NagoyaTripApp;
