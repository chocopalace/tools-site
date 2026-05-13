import React, { useRef, useState } from "react";
import { createWorker } from "tesseract.js";
import {
  Upload,
  Car,
  Phone,
  MapPin,
  Home,
  User,
  AlertTriangle,
  X,
  CircleDot,
  Loader2,
  ScanSearch,
  ShieldCheck,
  Type,
} from "lucide-react";

const riskTypes = [
  {
    id: "face",
    label: "顔",
    icon: User,
    color: "border-red-500",
    bg: "bg-red-50",
    text: "text-red-700",
  },
  {
    id: "plate",
    label: "車のナンバー",
    icon: Car,
    color: "border-orange-500",
    bg: "bg-orange-50",
    text: "text-orange-700",
  },
  {
    id: "phone",
    label: "電話番号",
    icon: Phone,
    color: "border-yellow-500",
    bg: "bg-yellow-50",
    text: "text-yellow-700",
  },
  {
    id: "address",
    label: "住所・表札",
    icon: Home,
    color: "border-pink-500",
    bg: "bg-pink-50",
    text: "text-pink-700",
  },
  {
    id: "location",
    label: "場所特定のヒント",
    icon: MapPin,
    color: "border-blue-500",
    bg: "bg-blue-50",
    text: "text-blue-700",
  },
  {
    id: "text",
    label: "文字情報",
    icon: Type,
    color: "border-purple-500",
    bg: "bg-purple-50",
    text: "text-purple-700",
  },
];

const locationWords = [
  "駅",
  "学校",
  "小学校",
  "中学校",
  "高校",
  "幼稚園",
  "保育園",
  "病院",
  "医院",
  "クリニック",
  "公園",
  "市",
  "区",
  "町",
  "丁目",
  "番地",
  "交差点",
  "店",
  "支店",
  "営業所",
  "株式会社",
];

function getRiskTypeFromText(text) {
  const normalized = text.replace(/\s/g, "");

  if (/0\d{1,4}[-ー−]?\d{1,4}[-ー−]?\d{3,4}/.test(normalized)) {
    return "phone";
  }

  if (/\d{3}[-ー−]?\d{4}/.test(normalized)) {
    return "address";
  }

  if (/(都|道|府|県|市|区|町|村|丁目|番地|号)/.test(normalized)) {
    return "address";
  }

  if (locationWords.some((word) => normalized.includes(word))) {
    return "location";
  }

  if (/[ぁ-んァ-ヶ一-龠A-Za-z0-9]{3,}/.test(normalized)) {
    return "text";
  }

  return null;
}

function clampPercent(value) {
  return Math.max(0, Math.min(100, value));
}

export default function App() {
  const [image, setImage] = useState(null);
  const [imageFile, setImageFile] = useState(null);
  const [marks, setMarks] = useState([]);
  const [ocrText, setOcrText] = useState("");
  const [isChecking, setIsChecking] = useState(false);
  const [progress, setProgress] = useState(0);
  const [message, setMessage] = useState(
    "写真を選んで自動チェックしてください"
  );

  const fileRef = useRef(null);

  const handleFile = (event) => {
    const file = event.target.files?.[0];
    if (!file) return;

    const url = URL.createObjectURL(file);

    setImage(url);
    setImageFile(file);
    setMarks([]);
    setOcrText("");
    setMessage("画像を読み込みました");
  };

  const detectTextRisks = async () => {
    if (!imageFile) return [];

    const worker = await createWorker("jpn+eng", 1, {
      logger: (m) => {
        if (m.status === "recognizing text") {
          setProgress(Math.round(m.progress * 100));
        }
      },
    });

    const result = await worker.recognize(imageFile);

    await worker.terminate();

    const text = result?.data?.text || "";
    setOcrText(text);

    const words = result?.data?.words || [];

    const detected = [];

    words.forEach((word, index) => {
      const raw = word.text || "";

      const type = getRiskTypeFromText(raw);

      if (!type || !word.bbox) return;

      const { x0, y0, x1, y1 } = word.bbox;

      detected.push({
        id: `text-${index}`,
        type,
        x: clampPercent(x0 / 10),
        y: clampPercent(y0 / 10),
        w: clampPercent((x1 - x0) / 10),
        h: clampPercent((y1 - y0) / 10),
        memo: `${raw} が写っています`,
      });
    });

    return detected;
  };

  const runAutoCheck = async () => {
    if (!imageFile) return;

    setIsChecking(true);
    setMessage("画像を解析中...");

    try {
      const detected = await detectTextRisks();

      setMarks(detected);

      if (detected.length === 0) {
        setMessage("危険箇所は見つかりませんでした");
      } else {
        setMessage(`${detected.length} 件の危険候補を検出`);
      }
    } catch (e) {
      setMessage("エラーが発生しました");
    } finally {
      setIsChecking(false);
    }
  };

  return (
    <div className="min-h-screen bg-slate-100 p-6">
      <div className="mx-auto max-w-6xl">
        <h1 className="mb-4 text-4xl font-bold">
          SNS写真 危険チェック
        </h1>

        <div className="mb-4 flex gap-3">
          <input
            ref={fileRef}
            type="file"
            accept="image/*"
            className="hidden"
            onChange={handleFile}
          />

          <button
            onClick={() => fileRef.current?.click()}
            className="rounded bg-blue-600 px-4 py-2 text-white"
          >
            <Upload className="mr-2 inline h-4 w-4" />
            写真を選ぶ
          </button>

          <button
            onClick={runAutoCheck}
            disabled={!image || isChecking}
            className="rounded bg-black px-4 py-2 text-white disabled:opacity-50"
          >
            {isChecking ? (
              <Loader2 className="mr-2 inline h-4 w-4 animate-spin" />
            ) : (
              <ScanSearch className="mr-2 inline h-4 w-4" />
            )}
            自動チェック
          </button>
        </div>

        <div className="mb-4 rounded bg-white p-4 shadow">
          <p>{message}</p>

          {isChecking && (
            <div className="mt-2 h-2 w-full overflow-hidden rounded bg-gray-200">
              <div
                className="h-full bg-blue-600"
                style={{ width: `${progress}%` }}
              />
            </div>
          )}
        </div>

        <div className="grid gap-6 lg:grid-cols-2">
          <div className="rounded bg-white p-4 shadow">
            {!image ? (
              <div className="flex h-[500px] items-center justify-center text-gray-400">
                <div className="text-center">
                  <CircleDot className="mx-auto mb-2 h-10 w-10" />
                  写真を選択してください
                </div>
              </div>
            ) : (
              <div className="relative">
                <img
                  src={image}
                  alt="preview"
                  className="w-full rounded"
                />

                {marks.map((mark) => {
                  const risk =
                    riskTypes.find((r) => r.id === mark.type) ||
                    riskTypes[0];

                  return (
                    <div
                      key={mark.id}
                      className={`absolute rounded-full border-4 ${risk.color}`}
                      style={{
                        left: `${mark.x}%`,
                        top: `${mark.y}%`,
                        width: `${Math.max(mark.w, 8)}%`,
                        height: `${Math.max(mark.h, 6)}%`,
                      }}
                    >
                      <div
                        className={`absolute -top-7 left-0 rounded px-2 py-1 text-xs ${risk.bg} ${risk.text}`}
                      >
                        {risk.label}
                      </div>
                    </div>
                  );
                })}
              </div>
            )}
          </div>

          <div className="space-y-4">
            <div className="rounded bg-white p-4 shadow">
              <h2 className="mb-3 flex items-center gap-2 text-xl font-bold">
                <ShieldCheck className="h-5 w-5" />
                検出された危険候補
              </h2>

              {marks.length === 0 ? (
                <p className="text-gray-500">
                  まだ検出結果はありません
                </p>
              ) : (
                <div className="space-y-2">
                  {marks.map((mark) => {
                    const risk =
                      riskTypes.find((r) => r.id === mark.type) ||
                      riskTypes[0];

                    const Icon = risk.icon;

                    return (
                      <div
                        key={mark.id}
                        className="flex items-start gap-3 rounded border p-3"
                      >
                        <Icon className="mt-1 h-5 w-5" />

                        <div className="flex-1">
                          <div className="font-bold">
                            {risk.label}
                          </div>

                          <div className="text-sm text-gray-500">
                            {mark.memo}
                          </div>
                        </div>

                        <button
                          onClick={() =>
                            setMarks((prev) =>
                              prev.filter((m) => m.id !== mark.id)
                            )
                          }
                        >
                          <X className="h-4 w-4" />
                        </button>
                      </div>
                    );
                  })}
                </div>
              )}
            </div>

            <div className="rounded bg-black p-4 text-white shadow">
              <h2 className="mb-3 text-xl font-bold">
                OCR読み取り結果
              </h2>

              <div className="max-h-64 overflow-auto whitespace-pre-wrap rounded bg-white/10 p-3 text-sm">
                {ocrText || "まだOCR結果はありません"}
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  );
}
