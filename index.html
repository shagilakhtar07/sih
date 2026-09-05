import React, { useState, useMemo, useEffect } from "react";
import {
  MapPin, Train, Plane, Bus, Hotel, Car, Ticket, ArrowRight, ArrowLeft,
  Clock, Star, ShoppingBag, X, Check, Sparkles, CloudSun, Users, AlertTriangle,
  BookOpen, Loader2
} from "lucide-react";

// ---------- Design tokens ----------
const C = {
  deep: "#065A82",
  teal: "#1C7293",
  mid: "#21295C",
  ink: "#101B33",
  muted: "#5C7A8A",
  ice: "#EAF4F8",
  canvas: "#F6F9FB",
  gold: "#F2A93B",
  goldDeep: "#D98E1E",
  card: "#FFFFFF",
  good: "#1E7A3E",
};

const serif = '"Cambria", Georgia, "Times New Roman", serif';
const sans = 'ui-sans-serif, -apple-system, "Segoe UI", system-ui, sans-serif';

// ---------- Mock data ----------
const DESTINATIONS = ["Manali, HP", "Jaipur, RJ", "Goa", "Rishikesh, UK", "Udaipur, RJ"];

const TRANSPORT = {
  train: [
    { id: "t1", name: "Dehradun – Kalka Exp", dep: "06:20", arr: "13:10", dur: "6h 50m", price: 480, tag: "Sleeper" },
    { id: "t2", name: "Shatabdi Express", dep: "07:05", arr: "12:40", dur: "5h 35m", price: 1150, tag: "AC Chair" },
  ],
  flight: [
    { id: "f1", name: "IndiGo 6E-204", dep: "09:15", arr: "10:35", dur: "1h 20m", price: 4200, tag: "Non-stop" },
    { id: "f2", name: "Air India AI-441", dep: "14:00", arr: "15:30", dur: "1h 30m", price: 3850, tag: "Non-stop" },
  ],
  bus: [
    { id: "b1", name: "Volvo AC Sleeper", dep: "21:30", arr: "07:00", dur: "9h 30m", price: 950, tag: "Sleeper" },
    { id: "b2", name: "Himachal RTC", dep: "22:15", arr: "08:45", dur: "10h 30m", price: 620, tag: "Semi-sleeper" },
  ],
};

const HOTELS = [
  { id: "h1", name: "Snow Valley Resort", rating: 4.4, price: 2600, note: "1.2 km from mall road" },
  { id: "h2", name: "Riverside Homestay", rating: 4.7, price: 1450, note: "On the Beas riverbank" },
  { id: "h3", name: "Hotel Mountain Pearl", rating: 4.1, price: 1900, note: "Free breakfast included" },
];

const ATTRACTIONS = [
  { id: "a1", name: "Solang Valley Ropeway", price: 700, note: "Cable car + adventure zone" },
  { id: "a2", name: "Hadimba Temple", price: 0, note: "Free entry, guided tour ₹150" },
  { id: "a3", name: "Old Manali Walking Tour", price: 350, note: "2 hr guided heritage walk" },
];

const CABS = [
  { id: "c1", name: "Airport/Station Pickup", price: 550, note: "Sedan, up to 4 passengers" },
  { id: "c2", name: "Full-day Local Sightseeing", price: 1800, note: "8 hrs / 80 km, SUV" },
];

const TABS = [
  { id: "transport", label: "Transport", icon: Train },
  { id: "stay", label: "Stay", icon: Hotel },
  { id: "attractions", label: "Attractions", icon: Ticket },
  { id: "cab", label: "Local Cabs", icon: Car },
];

const modeIcon = { train: Train, flight: Plane, bus: Bus };

// ---------- AI insights (calls Claude with web search for live context) ----------
async function fetchInsights(destination) {
  const prompt = `You are a travel-insights engine for a trip-planning app called EasyTour. The traveller is heading to "${destination}" in India, arriving soon. Use web search to check the current/upcoming weather forecast and any known crowd patterns or seasonal tourist volume for this destination right now.

Respond with ONLY a raw JSON object (no markdown, no backticks, no commentary) matching exactly this shape:
{
  "weather_now": "short phrase, e.g. '14°C, partly cloudy'",
  "weather_advisory": "1 short sentence of practical advice for a traveller, warm and helpful tone",
  "crowd_level": "Low or Moderate or High",
  "crowd_note": "1 short sentence explaining why, tied to season/day/festival if relevant",
  "possible_issues": ["short issue 1", "short issue 2", "short issue 3"],
  "history_summary": "2-3 sentence original summary in your own words of the place's history and why it's worth visiting, do not quote any source verbatim",
  "enjoyment_note": "1 short upbeat sentence on who would enjoy this and what makes it special"
}
Keep every string field concise, under 25 words each. Base weather and crowd fields on what you find via search; if search results are thin, give a reasonable seasonal estimate and say so briefly within the field.`;

  const response = await fetch("https://api.anthropic.com/v1/messages", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({
      model: "claude-sonnet-4-6",
      max_tokens: 1000,
      tools: [{ type: "web_search_20250305", name: "web_search" }],
      messages: [{ role: "user", content: prompt }],
    }),
  });
  const data = await response.json();
  const text = (data.content || [])
    .map((block) => (block.type === "text" ? block.text : ""))
    .filter(Boolean)
    .join("\n");
  const clean = text.replace(/```json|```/g, "").trim();
  return JSON.parse(clean);
}

// ---------- App ----------
export default function App() {
  const [screen, setScreen] = useState("home"); // home | results | confirm
  const [origin, setOrigin] = useState("Dehradun, UK");
  const [destination, setDestination] = useState("Manali, HP");
  const [activeTab, setActiveTab] = useState("transport");
  const [transportMode, setTransportMode] = useState("train");
  const [cart, setCart] = useState([]);
  const [aiInsights, setAiInsights] = useState(null);
  const [aiLoading, setAiLoading] = useState(false);
  const [aiError, setAiError] = useState(false);

  const total = useMemo(() => cart.reduce((s, i) => s + i.price, 0), [cart]);

  useEffect(() => {
    if (screen !== "results") return;
    let cancelled = false;
    setAiInsights(null);
    setAiError(false);
    setAiLoading(true);
    fetchInsights(destination)
      .then((data) => { if (!cancelled) setAiInsights(data); })
      .catch(() => { if (!cancelled) setAiError(true); })
      .finally(() => { if (!cancelled) setAiLoading(false); });
    return () => { cancelled = true; };
  }, [screen, destination]);

  function addToCart(category, item) {
    setCart((prev) => {
      const withoutCategory = prev.filter((i) => i.category !== category);
      return [...withoutCategory, { ...item, category }];
    });
  }
  function removeFromCart(category) {
    setCart((prev) => prev.filter((i) => i.category !== category));
  }
  function inCart(category, id) {
    return cart.some((i) => i.category === category && i.id === id);
  }

  return (
    <div style={{ fontFamily: sans, background: C.canvas, minHeight: "100%", color: C.ink }}>
      <style>{`
        * { box-sizing: border-box; }
        button { font-family: ${sans}; cursor: pointer; }
        .btn-primary {
          background: ${C.deep}; color: white; border: none; border-radius: 10px;
          padding: 12px 22px; font-weight: 600; font-size: 14px;
          display: inline-flex; align-items: center; gap: 8px; transition: background .15s ease;
        }
        .btn-primary:hover { background: ${C.mid}; }
        .btn-ghost {
          background: transparent; color: ${C.deep}; border: 1.5px solid ${C.deep};
          border-radius: 10px; padding: 10px 18px; font-weight: 600; font-size: 13.5px;
          display: inline-flex; align-items: center; gap: 6px;
        }
        .tab-btn {
          border: none; background: transparent; padding: 10px 16px; border-radius: 999px;
          font-size: 13.5px; font-weight: 600; color: ${C.muted}; display: flex; align-items: center; gap: 7px;
        }
        .tab-btn.active { background: ${C.deep}; color: white; }
        .mode-btn {
          border: 1.5px solid ${C.ice}; background: white; padding: 8px 16px; border-radius: 8px;
          font-size: 13px; font-weight: 600; color: ${C.muted}; display: flex; align-items: center; gap: 6px;
        }
        .mode-btn.active { border-color: ${C.teal}; background: ${C.ice}; color: ${C.deep}; }
        .option-card {
          background: white; border-radius: 12px; padding: 16px 18px; display: flex;
          align-items: center; justify-content: space-between; gap: 16px;
          border: 1px solid #E7EEF2;
        }
        .add-btn {
          border: 1.5px solid ${C.teal}; background: white; color: ${C.teal}; border-radius: 8px;
          padding: 8px 14px; font-weight: 700; font-size: 12.5px; white-space: nowrap;
        }
        .add-btn.added { background: ${C.good}; border-color: ${C.good}; color: white; }
        input[type=text] { font-family: ${sans}; }
      `}</style>

      {screen === "home" && (
        <HomeScreen
          origin={origin} setOrigin={setOrigin}
          destination={destination} setDestination={setDestination}
          onSearch={() => setScreen("results")}
        />
      )}

      {screen === "results" && (
        <ResultsScreen
          origin={origin} destination={destination}
          activeTab={activeTab} setActiveTab={setActiveTab}
          transportMode={transportMode} setTransportMode={setTransportMode}
          cart={cart} total={total}
          addToCart={addToCart} removeFromCart={removeFromCart} inCart={inCart}
          onBack={() => setScreen("home")}
          onCheckout={() => setScreen("confirm")}
          aiInsights={aiInsights} aiLoading={aiLoading} aiError={aiError}
        />
      )}

      {screen === "confirm" && (
        <ConfirmScreen
          destination={destination} cart={cart} total={total}
          onNewSearch={() => { setCart([]); setScreen("home"); }}
        />
      )}
    </div>
  );
}

// ---------- Home screen ----------
function HomeScreen({ origin, setOrigin, destination, setDestination, onSearch }) {
  return (
    <div style={{ minHeight: "100vh", display: "flex", flexDirection: "column" }}>
      <div style={{
        background: `linear-gradient(135deg, ${C.mid} 0%, ${C.deep} 100%)`,
        padding: "48px 24px 64px", color: "white", position: "relative", overflow: "hidden",
      }}>
        <div style={{
          position: "absolute", top: -60, right: -40, width: 220, height: 220, borderRadius: "50%",
          background: "rgba(255,255,255,0.06)",
        }} />
        <div style={{ maxWidth: 760, margin: "0 auto", position: "relative" }}>
          <div style={{ display: "flex", alignItems: "center", gap: 8, marginBottom: 18 }}>
            <div style={{
              width: 30, height: 30, borderRadius: 8, background: C.gold,
              display: "flex", alignItems: "center", justifyContent: "center",
            }}>
              <MapPin size={17} color={C.mid} strokeWidth={2.5} />
            </div>
            <span style={{ fontWeight: 700, fontSize: 15, letterSpacing: 0.3 }}>EasyTour</span>
          </div>
          <h1 style={{ fontFamily: serif, fontSize: 38, lineHeight: 1.15, margin: "0 0 12px", maxWidth: 520 }}>
            Every ticket for your trip, from one search.
          </h1>
          <p style={{ fontSize: 15, color: "#CFE3ED", margin: "0 0 32px", maxWidth: 480 }}>
            Tell us where you're starting and where you're headed — trains, flights, buses, stays, cabs and local attraction tickets, all in one place.
          </p>

          <div style={{
            background: "white", borderRadius: 16, padding: 20, display: "flex",
            flexDirection: "column", gap: 14, boxShadow: "0 20px 50px rgba(10,30,50,0.25)",
          }}>
            <div style={{ display: "flex", gap: 12, flexWrap: "wrap" }}>
              <FieldBox label="From" value={origin} onChange={setOrigin} color={C.ink} />
              <div style={{ display: "flex", alignItems: "center", color: C.muted }}>
                <ArrowRight size={18} />
              </div>
              <FieldBox label="To" value={destination} onChange={setDestination} color={C.ink} isDestination />
            </div>
            <button className="btn-primary" style={{ justifyContent: "center", padding: "13px 22px" }} onClick={onSearch}>
              Search everything for this trip <ArrowRight size={16} />
            </button>
          </div>
        </div>
      </div>

      <div style={{ maxWidth: 760, margin: "0 auto", padding: "36px 24px", width: "100%" }}>
        <p style={{ fontSize: 12.5, color: C.muted, fontWeight: 600, marginBottom: 14 }}>POPULAR DESTINATIONS RIGHT NOW</p>
        <div style={{ display: "flex", gap: 10, flexWrap: "wrap" }}>
          {DESTINATIONS.map((d) => (
            <button key={d} className="mode-btn" onClick={() => setDestination(d)}
              style={{ borderRadius: 999, padding: "9px 16px" }}>
              {d}
            </button>
          ))}
        </div>
      </div>
    </div>
  );
}

function FieldBox({ label, value, onChange, isDestination }) {
  return (
    <div style={{ flex: 1, minWidth: 180 }}>
      <label style={{ fontSize: 11, fontWeight: 700, color: C.muted, display: "block", marginBottom: 4 }}>{label}</label>
      <div style={{ display: "flex", alignItems: "center", gap: 8, borderBottom: `2px solid ${isDestination ? C.gold : C.ice}`, paddingBottom: 6 }}>
        <MapPin size={15} color={isDestination ? C.goldDeep : C.muted} />
        <input
          type="text" value={value} onChange={(e) => onChange(e.target.value)}
          style={{ border: "none", outline: "none", fontSize: 14.5, fontWeight: 600, color: C.ink, width: "100%" }}
        />
      </div>
    </div>
  );
}

// ---------- Results screen ----------
function ResultsScreen({
  origin, destination, activeTab, setActiveTab, transportMode, setTransportMode,
  cart, total, addToCart, removeFromCart, inCart, onBack, onCheckout,
  aiInsights, aiLoading, aiError,
}) {
  return (
    <div style={{ paddingBottom: cart.length ? 110 : 40 }}>
      <div style={{ background: C.mid, color: "white", padding: "20px 24px" }}>
        <div style={{ maxWidth: 900, margin: "0 auto" }}>
          <button onClick={onBack} className="btn-ghost" style={{ borderColor: "rgba(255,255,255,0.4)", color: "white", marginBottom: 14, padding: "6px 12px", fontSize: 12.5 }}>
            <ArrowLeft size={13} /> Edit search
          </button>
          <div style={{ display: "flex", alignItems: "center", gap: 10, fontFamily: serif, fontSize: 22 }}>
            <span>{origin}</span>
            <ArrowRight size={16} color={C.gold} />
            <span>{destination}</span>
          </div>
        </div>
      </div>

      <div style={{ maxWidth: 900, margin: "0 auto", padding: "20px 24px" }}>
        <InsightsCard destination={destination} data={aiInsights} loading={aiLoading} error={aiError} />

        <div style={{ display: "flex", gap: 6, background: "white", padding: 6, borderRadius: 999, width: "fit-content", marginBottom: 22, border: `1px solid #E7EEF2` }}>
          {TABS.map((t) => (
            <button key={t.id} className={`tab-btn ${activeTab === t.id ? "active" : ""}`} onClick={() => setActiveTab(t.id)}>
              <t.icon size={15} /> {t.label}
            </button>
          ))}
        </div>

        {activeTab === "transport" && (
          <div>
            <div style={{ display: "flex", gap: 8, marginBottom: 16 }}>
              {["train", "flight", "bus"].map((m) => {
                const Icon = modeIcon[m];
                return (
                  <button key={m} className={`mode-btn ${transportMode === m ? "active" : ""}`} onClick={() => setTransportMode(m)}>
                    <Icon size={14} /> {m[0].toUpperCase() + m.slice(1)}
                  </button>
                );
              })}
            </div>
            <OptionList
              items={TRANSPORT[transportMode]}
              category="transport"
              renderMeta={(item) => (
                <div style={{ display: "flex", gap: 16, fontSize: 12.5, color: C.muted, marginTop: 4 }}>
                  <span>{item.dep} → {item.arr}</span>
                  <span style={{ display: "flex", alignItems: "center", gap: 4 }}><Clock size={12} /> {item.dur}</span>
                  <span>{item.tag}</span>
                </div>
              )}
              addToCart={addToCart} removeFromCart={removeFromCart} inCart={inCart}
            />
          </div>
        )}

        {activeTab === "stay" && (
          <OptionList
            items={HOTELS} category="stay"
            renderMeta={(item) => (
              <div style={{ display: "flex", gap: 14, fontSize: 12.5, color: C.muted, marginTop: 4 }}>
                <span style={{ display: "flex", alignItems: "center", gap: 4 }}><Star size={12} color={C.gold} fill={C.gold} /> {item.rating}</span>
                <span>{item.note}</span>
              </div>
            )}
            addToCart={addToCart} removeFromCart={removeFromCart} inCart={inCart}
            priceSuffix="/night"
          />
        )}

        {activeTab === "attractions" && (
          <div>
            <div style={{
              display: "flex", alignItems: "center", gap: 8, background: C.ice, color: C.deep,
              padding: "10px 14px", borderRadius: 10, fontSize: 12.5, fontWeight: 600, marginBottom: 16,
            }}>
              <Sparkles size={14} /> Suggested automatically from your destination — no separate search needed
            </div>
            <OptionList
              items={ATTRACTIONS} category="attractions"
              renderMeta={(item) => <div style={{ fontSize: 12.5, color: C.muted, marginTop: 4 }}>{item.note}</div>}
              addToCart={addToCart} removeFromCart={removeFromCart} inCart={inCart}
              freeLabel
            />
          </div>
        )}

        {activeTab === "cab" && (
          <OptionList
            items={CABS} category="cab"
            renderMeta={(item) => <div style={{ fontSize: 12.5, color: C.muted, marginTop: 4 }}>{item.note}</div>}
            addToCart={addToCart} removeFromCart={removeFromCart} inCart={inCart}
          />
        )}
      </div>

      {cart.length > 0 && (
        <CartBar cart={cart} total={total} onCheckout={onCheckout} />
      )}
    </div>
  );
}

const crowdColor = { Low: C.good, Moderate: C.goldDeep, High: "#C0392B" };

function InsightsCard({ destination, data, loading, error }) {
  return (
    <div style={{
      background: "white", borderRadius: 14, border: "1px solid #E7EEF2",
      padding: "20px 22px", marginBottom: 22,
    }}>
      <div style={{ display: "flex", alignItems: "center", gap: 8, marginBottom: loading || error ? 0 : 16 }}>
        <div style={{
          width: 28, height: 28, borderRadius: 8, background: C.ice,
          display: "flex", alignItems: "center", justifyContent: "center",
        }}>
          <Sparkles size={15} color={C.deep} />
        </div>
        <span style={{ fontWeight: 700, fontSize: 14.5 }}>AI trip insights for {destination}</span>
      </div>

      {loading && (
        <div style={{ display: "flex", alignItems: "center", gap: 8, color: C.muted, fontSize: 13, padding: "14px 2px 4px" }}>
          <Loader2 size={15} className="spin" />
          Checking live weather, crowd patterns and local history…
          <style>{`.spin { animation: spin 1s linear infinite; } @keyframes spin { to { transform: rotate(360deg); } }`}</style>
        </div>
      )}

      {error && !loading && (
        <div style={{ color: C.muted, fontSize: 13, padding: "14px 2px 4px" }}>
          Couldn't load live insights right now — you can still browse and book below.
        </div>
      )}

      {data && !loading && !error && (
        <div style={{ display: "flex", flexDirection: "column", gap: 16 }}>
          <InsightRow icon={CloudSun} title={data.weather_now}>
            {data.weather_advisory}
          </InsightRow>

          <InsightRow
            icon={Users}
            title={<span>Crowd level: <span style={{ color: crowdColor[data.crowd_level] || C.deep }}>{data.crowd_level}</span></span>}
          >
            {data.crowd_note}
          </InsightRow>

          {Array.isArray(data.possible_issues) && data.possible_issues.length > 0 && (
            <InsightRow icon={AlertTriangle} title="Things to watch out for">
              <ul style={{ margin: "2px 0 0", paddingLeft: 16 }}>
                {data.possible_issues.map((issue, i) => (
                  <li key={i} style={{ fontSize: 13, color: C.muted, marginBottom: 2 }}>{issue}</li>
                ))}
              </ul>
            </InsightRow>
          )}

          <InsightRow icon={BookOpen} title="History & why visit">
            {data.history_summary}
          </InsightRow>

          {data.enjoyment_note && (
            <div style={{
              background: C.ice, borderRadius: 10, padding: "10px 14px", fontSize: 13,
              color: C.deep, fontStyle: "italic",
            }}>
              {data.enjoyment_note}
            </div>
          )}
        </div>
      )}
    </div>
  );
}

function InsightRow({ icon: Icon, title, children }) {
  return (
    <div style={{ display: "flex", gap: 12 }}>
      <div style={{
        width: 30, height: 30, borderRadius: 8, background: C.canvas, flexShrink: 0,
        display: "flex", alignItems: "center", justifyContent: "center",
      }}>
        <Icon size={15} color={C.teal} />
      </div>
      <div>
        <div style={{ fontWeight: 700, fontSize: 13.5, marginBottom: 2 }}>{title}</div>
        <div style={{ fontSize: 13, color: C.muted, lineHeight: 1.45 }}>{children}</div>
      </div>
    </div>
  );
}

function OptionList({ items, category, renderMeta, addToCart, removeFromCart, inCart, priceSuffix = "", freeLabel = false }) {
  return (
    <div style={{ display: "flex", flexDirection: "column", gap: 10 }}>
      {items.map((item) => {
        const added = inCart(category, item.id);
        return (
          <div key={item.id} className="option-card">
            <div>
              <div style={{ fontWeight: 700, fontSize: 14.5 }}>{item.name}</div>
              {renderMeta(item)}
            </div>
            <div style={{ display: "flex", alignItems: "center", gap: 16 }}>
              <div style={{ textAlign: "right" }}>
                <div style={{ fontWeight: 700, fontSize: 15, color: C.ink }}>
                  {item.price === 0 && freeLabel ? "Free" : `₹${item.price.toLocaleString("en-IN")}`}
                </div>
                {priceSuffix && item.price > 0 && <div style={{ fontSize: 10.5, color: C.muted }}>{priceSuffix}</div>}
              </div>
              <button
                className={`add-btn ${added ? "added" : ""}`}
                onClick={() => (added ? removeFromCart(category) : addToCart(category, item))}
              >
                {added ? (<span style={{ display: "flex", alignItems: "center", gap: 5 }}><Check size={13} /> Added</span>) : "Add to trip"}
              </button>
            </div>
          </div>
        );
      })}
    </div>
  );
}

function CartBar({ cart, total, onCheckout }) {
  return (
    <div style={{
      position: "fixed", bottom: 0, left: 0, right: 0, background: C.mid, color: "white",
      padding: "14px 24px", display: "flex", justifyContent: "center",
      boxShadow: "0 -8px 24px rgba(0,0,0,0.15)",
    }}>
      <div style={{ maxWidth: 900, width: "100%", display: "flex", alignItems: "center", justifyContent: "space-between", gap: 16, flexWrap: "wrap" }}>
        <div style={{ display: "flex", alignItems: "center", gap: 10 }}>
          <ShoppingBag size={18} color={C.gold} />
          <div>
            <div style={{ fontSize: 13, fontWeight: 700 }}>{cart.length} item{cart.length > 1 ? "s" : ""} in your trip</div>
            <div style={{ fontSize: 11.5, color: "#B9CBD5" }}>{cart.map((i) => i.name).join(" · ")}</div>
          </div>
        </div>
        <div style={{ display: "flex", alignItems: "center", gap: 18 }}>
          <div style={{ fontFamily: serif, fontSize: 20 }}>₹{total.toLocaleString("en-IN")}</div>
          <button className="btn-primary" style={{ background: C.gold, color: C.mid }} onClick={onCheckout}>
            Book all <ArrowRight size={15} />
          </button>
        </div>
      </div>
    </div>
  );
}

// ---------- Confirmation screen ----------
function ConfirmScreen({ destination, cart, total, onNewSearch }) {
  return (
    <div style={{ maxWidth: 640, margin: "0 auto", padding: "60px 24px", textAlign: "center" }}>
      <div style={{
        width: 64, height: 64, borderRadius: "50%", background: C.ice, display: "flex",
        alignItems: "center", justifyContent: "center", margin: "0 auto 20px",
      }}>
        <Check size={30} color={C.deep} strokeWidth={2.5} />
      </div>
      <h2 style={{ fontFamily: serif, fontSize: 28, margin: "0 0 8px" }}>Your trip to {destination} is booked</h2>
      <p style={{ color: C.muted, fontSize: 14, margin: "0 0 32px" }}>One confirmation, one itinerary — for every ticket below.</p>

      <div style={{ background: "white", borderRadius: 14, border: "1px dashed #C7D9E2", padding: "22px 24px", textAlign: "left" }}>
        {cart.map((item, idx) => (
          <div key={item.category} style={{
            display: "flex", justifyContent: "space-between", padding: "12px 0",
            borderBottom: idx < cart.length - 1 ? "1px solid #EEF3F6" : "none",
          }}>
            <div>
              <div style={{ fontSize: 11, color: C.muted, fontWeight: 700, textTransform: "capitalize" }}>{item.category}</div>
              <div style={{ fontWeight: 700, fontSize: 14.5 }}>{item.name}</div>
            </div>
            <div style={{ fontWeight: 700, alignSelf: "center" }}>
              {item.price === 0 ? "Free" : `₹${item.price.toLocaleString("en-IN")}`}
            </div>
          </div>
        ))}
        <div style={{ display: "flex", justifyContent: "space-between", paddingTop: 16, marginTop: 6, borderTop: `2px solid ${C.ink}` }}>
          <div style={{ fontWeight: 700 }}>Total paid</div>
          <div style={{ fontFamily: serif, fontSize: 20 }}>₹{total.toLocaleString("en-IN")}</div>
        </div>
      </div>

      <button className="btn-primary" style={{ marginTop: 28 }} onClick={onNewSearch}>
        Plan another trip
      </button>
    </div>
  );
}
