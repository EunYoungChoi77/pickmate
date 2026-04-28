import React, { useState, useEffect } from 'react';
import { ChevronRight, RefreshCw, Check, Zap, Info, ArrowLeft, BrainCircuit } from 'lucide-react';

const App = () => {
  const [step, setStep] = useState(0); // 0: Home, 1: Inputs, 2: Criteria, 3: Loading, 4: Result
  const [formData, setFormData] = useState({
    topic: '',
    optionA: '',
    optionB: '',
    criteria: []
  });
  const [result, setResult] = useState(null);

  const criteriaList = [
    '비용', '시간', '만족도', '감정', '효율', '건강', '장기적 이익'
  ];

  const handleNext = () => setStep(step + 1);
  const handleBack = () => setStep(step - 1);

  const toggleCriteria = (item) => {
    setFormData(prev => ({
      ...prev,
      criteria: prev.criteria.includes(item)
        ? prev.criteria.filter(i => i !== item)
        : [...prev.criteria, item]
    }));
  };

  const startAnalysis = () => {
    setStep(3);
    // Mock AI Analysis Delay
    setTimeout(() => {
      const winner = Math.random() > 0.5 ? formData.optionA : formData.optionB;
      const score = Math.floor(Math.random() * (95 - 75 + 1)) + 75;
      setResult({
        winner,
        score,
        reason: `${formData.criteria.join(', ')} 측면에서 분석했을 때, 현재 상황에서는 ${winner} 선택이 가장 합리적입니다. 특히 효율성과 만족도 면에서 높은 가중치가 부여되었습니다.`,
        prosA: '즉각적인 효과와 낮은 진입 장벽',
        consA: '장기적인 유지 비용 발생 가능성',
        prosB: '안정적인 결과와 높은 지속성',
        consB: '초기 시간 투자가 상대적으로 많음'
      });
      setStep(4);
    }, 2500);
  };

  const reset = () => {
    setFormData({ topic: '', optionA: '', optionB: '', criteria: [] });
    setStep(0);
  };

  // Components for each screen
  const ScreenWrapper = ({ children }) => (
    <div className="flex flex-col h-full max-w-[390px] mx-auto bg-white shadow-2xl min-h-screen overflow-hidden relative">
      {children}
    </div>
  );

  return (
    <div className="min-h-screen bg-slate-50 flex justify-center items-start sm:items-center">
      <ScreenWrapper>
        {/* Step 0: Home */}
        {step === 0 && (
          <div className="flex-1 flex flex-col items-center justify-center p-8 text-center animate-fadeIn">
            <div className="w-20 h-20 bg-gradient-to-tr from-[#4F8CFF] to-[#8B5CF6] rounded-3xl flex items-center justify-center mb-6 shadow-lg shadow-blue-200">
              <BrainCircuit size={40} color="white" />
            </div>
            <h1 className="text-4xl font-black text-slate-900 mb-2 tracking-tight">PickMate</h1>
            <p className="text-slate-500 font-medium mb-12">AI가 당신의 최선의 선택을 도와드릴게요</p>
            <button 
              onClick={handleNext}
              className="w-full py-4 bg-[#4F8CFF] text-white rounded-2xl font-bold text-lg shadow-lg hover:opacity-90 transition-all flex items-center justify-center gap-2"
            >
              선택 시작하기 <ChevronRight size={20} />
            </button>
          </div>
        )}

        {/* Step 1: Inputs */}
        {step === 1 && (
          <div className="flex-1 p-6 flex flex-col animate-fadeIn">
            <button onClick={handleBack} className="mb-6"><ArrowLeft size={24} className="text-slate-400" /></button>
            <h2 className="text-2xl font-bold text-slate-800 mb-8">무엇을 고민하고<br />계신가요?</h2>
            
            <div className="space-y-6 flex-1">
              <div className="bg-slate-50 p-4 rounded-2xl border border-slate-100">
                <label className="text-xs font-bold text-[#4F8CFF] uppercase mb-2 block">고민 주제</label>
                <input 
                  className="bg-transparent w-full outline-none text-slate-700 placeholder:text-slate-300"
                  placeholder="예: 오늘 점심 메뉴"
                  value={formData.topic}
                  onChange={(e) => setFormData({...formData, topic: e.target.value})}
                />
              </div>

              <div className="grid grid-cols-2 gap-4">
                <div className="bg-white p-4 rounded-2xl border-2 border-blue-50 shadow-sm">
                  <label className="text-xs font-bold text-blue-400 mb-2 block">선택지 A</label>
                  <input 
                    className="w-full outline-none text-slate-700 placeholder:text-slate-300 font-medium"
                    placeholder="짜장면"
                    value={formData.optionA}
                    onChange={(e) => setFormData({...formData, optionA: e.target.value})}
                  />
                </div>
                <div className="bg-white p-4 rounded-2xl border-2 border-purple-50 shadow-sm">
                  <label className="text-xs font-bold text-purple-400 mb-2 block">선택지 B</label>
                  <input 
                    className="w-full outline-none text-slate-700 placeholder:text-slate-300 font-medium"
                    placeholder="짬뽕"
                    value={formData.optionB}
                    onChange={(e) => setFormData({...formData, optionB: e.target.value})}
                  />
                </div>
              </div>
            </div>

            <button 
              disabled={!formData.optionA || !formData.optionB}
              onClick={handleNext}
              className="mt-auto py-4 bg-[#4F8CFF] disabled:bg-slate-200 text-white rounded-2xl font-bold text-lg shadow-lg"
            >
              다음
            </button>
          </div>
        )}

        {/* Step 2: Criteria */}
        {step === 2 && (
          <div className="flex-1 p-6 flex flex-col animate-fadeIn">
            <button onClick={handleBack} className="mb-6"><ArrowLeft size={24} className="text-slate-400" /></button>
            <h2 className="text-2xl font-bold text-slate-800 mb-2">중요한 기준을<br />선택하세요</h2>
            <p className="text-slate-400 text-sm mb-8">AI가 이 기준들을 바탕으로 분석합니다.</p>
            
            <div className="flex flex-wrap gap-3 flex-1 overflow-y-auto content-start">
              {criteriaList.map((item) => (
                <button
                  key={item}
                  onClick={() => toggleCriteria(item)}
                  className={`px-5 py-3 rounded-full font-semibold transition-all border ${
                    formData.criteria.includes(item)
                      ? 'bg-[#8B5CF6] border-[#8B5CF6] text-white shadow-md'
                      : 'bg-white border-slate-200 text-slate-500'
                  }`}
                >
                  {item}
                </button>
              ))}
            </div>

            <button 
              disabled={formData.criteria.length === 0}
              onClick={startAnalysis}
              className="mt-auto py-4 bg-gradient-to-r from-[#4F8CFF] to-[#8B5CF6] disabled:from-slate-200 disabled:to-slate-200 text-white rounded-2xl font-bold text-lg shadow-lg flex items-center justify-center gap-2"
            >
              <Zap size={20} fill="white" /> AI 분석하기
            </button>
          </div>
        )}

        {/* Step 3: Loading */}
        {step === 3 && (
          <div className="flex-1 flex flex-col items-center justify-center p-8 text-center animate-fadeIn">
            <div className="relative mb-8">
              <div className="w-16 h-16 border-4 border-slate-100 border-t-[#4F8CFF] rounded-full animate-spin"></div>
              <div className="absolute inset-0 flex items-center justify-center">
                <BrainCircuit size={24} className="text-[#8B5CF6]" />
              </div>
            </div>
            <h3 className="text-xl font-bold text-slate-800 mb-2 italic">AI가 선택지를 분석 중입니다...</h3>
            <p className="text-slate-400 text-sm">최적의 결과를 도출하고 있어요</p>
          </div>
        )}

        {/* Step 4: Result */}
        {step === 4 && (
          <div className="flex-1 p-6 flex flex-col bg-slate-50 animate-fadeIn overflow-y-auto">
            <div className="text-center mb-8 pt-4">
              <span className="bg-blue-100 text-[#4F8CFF] text-[10px] font-black px-3 py-1 rounded-full uppercase tracking-widest">Analysis Result</span>
              <h2 className="text-3xl font-black text-slate-900 mt-4 leading-tight">AI의 추천 결과는?</h2>
            </div>

            <div className="space-y-4 mb-8">
              {/* Card 1: Main Result */}
              <div className="bg-white p-6 rounded-[24px] shadow-sm border border-blue-50 relative overflow-hidden">
                <div className="absolute top-0 right-0 p-4 opacity-10"><Zap size={60} /></div>
                <p className="text-slate-400 text-sm font-medium mb-1">추천 선택지</p>
                <h3 className="text-4xl font-black text-[#4F8CFF] mb-2">{result.winner}</h3>
                <div className="flex items-center gap-2 mt-4">
                  <div className="flex-1 h-2 bg-slate-100 rounded-full overflow-hidden">
                    <div className="h-full bg-[#8B5CF6]" style={{width: `${result.score}%`}}></div>
                  </div>
                  <span className="text-sm font-bold text-[#8B5CF6]">{result.score}점</span>
                </div>
              </div>

              {/* Card 2: Reason */}
              <div className="bg-white p-6 rounded-[24px] shadow-sm border border-slate-100">
                <div className="flex items-center gap-2 mb-3">
                  <div className="w-8 h-8 bg-purple-50 rounded-lg flex items-center justify-center">
                    <Info size={16} className="text-[#8B5CF6]" />
                  </div>
                  <h4 className="font-bold text-slate-800">추천 이유</h4>
                </div>
                <p className="text-slate-600 text-sm leading-relaxed">{result.reason}</p>
              </div>

              {/* Card 3: Comparison */}
              <div className="bg-white p-6 rounded-[24px] shadow-sm border border-slate-100">
                <h4 className="font-bold text-slate-800 mb-4 flex items-center gap-2">
                   <div className="w-8 h-8 bg-blue-50 rounded-lg flex items-center justify-center text-[#4F8CFF]">VS</div>
                   상세 비교
                </h4>
                <div className="space-y-4">
                  <div className="bg-blue-50/50 p-3 rounded-xl">
                    <p className="text-xs font-bold text-[#4F8CFF] mb-1 italic">{formData.optionA}</p>
                    <p className="text-[13px] text-slate-600"><span className="text-blue-500 font-bold">+</span> {result.prosA}</p>
                    <p className="text-[13px] text-slate-600"><span className="text-red-400 font-bold">-</span> {result.consA}</p>
                  </div>
                  <div className="bg-purple-50/50 p-3 rounded-xl">
                    <p className="text-xs font-bold text-[#8B5CF6] mb-1 italic">{formData.optionB}</p>
                    <p className="text-[13px] text-slate-600"><span className="text-blue-500 font-bold">+</span> {result.prosB}</p>
                    <p className="text-[13px] text-slate-600"><span className="text-red-400 font-bold">-</span> {result.consB}</p>
                  </div>
                </div>
              </div>
            </div>

            <button 
              onClick={reset}
              className="py-4 bg-white border-2 border-slate-100 text-slate-600 rounded-2xl font-bold text-lg flex items-center justify-center gap-2 mb-4 hover:bg-slate-50 transition-colors"
            >
              <RefreshCw size={18} /> 다시 선택하기
            </button>
          </div>
        )}
      </ScreenWrapper>

      <style>{`
        @keyframes fadeIn {
          from { opacity: 0; transform: translateY(10px); }
          to { opacity: 1; transform: translateY(0); }
        }
        .animate-fadeIn {
          animation: fadeIn 0.4s ease-out forwards;
        }
      `}</style>
    </div>
  );
};

export default App;
