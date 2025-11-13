import React, { useState } from "react";

function App() {
  const [page, setPage] = useState("login");
  const [code, setCode] = useState("");
  const [isLogged, setIsLogged] = useState(false);
  const [startTime, setStartTime] = useState("");
  const [endTime, setEndTime] = useState("");

  const subjects = {
    "📚 عربي": ["محمد صلاح", "رضا الفاروق"],
    "🧮 رياضة": ["أحمد عصام", "لطفي زهران"],
    "🗣️ إنجليزي": [
      "ميس مي مجدي",
      "انجلشاوي",
      "عبدالحميد حامد",
      "شريف المصري",
      "وائل ميلاد",
      "عبقري اللغة",
    ],
    "🧬 أحياء": [
      "أحمد الجوهري",
      "محمد أيمن",
      "جيو ماجد",
      "سامح أحمد",
      "أحمد رضوان",
    ],
    "⚡ فيزياء": ["محمد عبدالمعبود", "حسام خليل", "كيرلس", "محمود مجدي"],
    "🧪 كيمياء": [
      "محمد عبدالجواد",
      "خالد صقر",
      "عبدالله حبشي",
      "عمرو الصيفي",
      "جون جهبذ",
    ],
  };

  const handleLogin = () => {
    if (code === "1234") {
      setIsLogged(true);
      setPage("home");
      const start = new Date();
      const end = new Date();
      end.setMonth(start.getMonth() + 1);
      setStartTime(start.toLocaleString());
      setEndTime(end.toLocaleString());
    } else {
      alert("رمز الدخول غير صحيح ❌");
    }
  };

  return (
    <div className="min-h-screen bg-gray-100 flex flex-col items-center p-5">
      {/* HEADER */}
      <h1 className="text-4xl font-bold text-red-600 mb-4">منصــة خطوتــك 🚀</h1>

      {/* LOGIN PAGE */}
      {page === "login" && !isLogged && (
        <div className="bg-white p-6 rounded-2xl shadow-md w-80 text-center">
          <h2 className="text-xl mb-3 text-gray-700">أدخل رمز الدخول</h2>
          <input
            type="password"
            className="border rounded w-full p-2 text-center"
            placeholder="••••"
            value={code}
            onChange={(e) => setCode(e.target.value)}
          />
          <button
            onClick={handleLogin}
            className="mt-4 w-full bg-red-500 text-white py-2 rounded-lg"
          >
            دخول
          </button>
          <p className="mt-3 text-sm text-gray-600">
            للتواصل 📞 01114672635
            <br />
            <a
              href="https://chat.whatsapp.com/HBZCFogEwom2l7kVErZvJE?mode=wwt"
              target="_blank"
              className="text-green-600 underline"
              rel="noreferrer"
            >
              تواصل على واتساب
            </a>
          </p>
        </div>
      )}

      {/* HOME PAGE */}
      {isLogged && page === "home" && (
        <div className="w-full max-w-md">
          <h2 className="text-2xl font-bold text-center mb-4">اختر المادة 📖</h2>
          <div className="grid grid-cols-2 gap-3">
            {Object.keys(subjects).map((subj) => (
              <button
                key={subj}
                onClick={() => setPage(subj)}
                className="bg-white shadow p-3 rounded-xl text-gray-800 hover:bg-red-100"
              >
                {subj}
              </button>
            ))}
          </div>

          <button
            className="mt-6 w-full bg-blue-500 text-white p-2 rounded-lg"
            onClick={() => setPage("subscription")}
          >
            💳 صفحة الاشتراك
          </button>
        </div>
      )}

      {/* SUBJECT PAGES */}
      {isLogged &&
        Object.keys(subjects).map(
          (subj) =>
            page === subj && (
              <div key={subj} className="w-full max-w-md text-center">
                <button
                  onClick={() => setPage("home")}
                  className="bg-gray-300 px-3 py-1 rounded mb-3"
                >
                  🔙 رجوع
                </button>
                <h2 className="text-2xl font-bold mb-3">{subj}</h2>
                <ul className="bg-white p-4 rounded-xl shadow">
                  {subjects[subj].map((teacher, index) => (
                    <li
                      key={index}
                      className="border-b py-2 text-lg text-gray-700 last:border-none"
                    >
                      {teacher}
                      <div className="text-sm text-gray-500">
                        الشهور: الأول | الثاني | الثالث | الرابع
                      </div>
                    </li>
                  ))}
                </ul>
              </div>
            )
        )}

      {/* SUBSCRIPTION PAGE */}
      {page === "subscription" && (
        <div className="bg-white p-5 rounded-2xl shadow-md w-80 text-center">
          <button
            onClick={() => setPage("home")}
            className="bg-gray-300 px-3 py-1 rounded mb-3"
          >
            🔙 رجوع
          </button>
          <h2 className="text-xl font-bold mb-2">💳 تفاصيل الاشتراك</h2>
          <p className="text-gray-700">
            السعر الشهري: <b>100 جنيه</b>
            <br />
            بدأ الاشتراك: {startTime}
            <br />
            ينتهي في: {endTime}
          </p>
        </div>
      )}
    </div>
  );
}

export default App;
