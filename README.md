import React, { useState, useEffect } from 'react';

function BitcoinPrice() {
  const [bitcoinData, setBitcoinData] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    async function fetchBitcoinPrice() {
      const url = 'https://api.coingecko.com/api/v3/simple/price?ids=bitcoin&vs_currencies=inr,usd&include_24hr_change=true';

      try {
        const response = await fetch(url);
        const data = await response.json();

        // Extract Bitcoin price data
        const bitcoinData = data.bitcoin;
        setBitcoinData(bitcoinData);
        setLoading(false);
      } catch (error) {
        console.error('Error fetching Bitcoin price:', error);
      }
    }

    fetchBitcoinPrice();
  }, []);

  return (
    <div>
      <h2>Bitcoin Price</h2>
      {loading ? (
        <p>Loading...</p>
      ) : (
        <div>
          <p>Price in USD: ${bitcoinData.usd}</p>
          <p>Price in INR: ₹{bitcoinData.inr}</p>
          <p>24-hour Change in USD: {bitcoinData.usd_24h_change}%</p>
        </div>
      )}
    </div>
  );
}

export default BitcoinPrice;
