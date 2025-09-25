import React, { useState } from 'react';
import { View, Text, Button, TextInput, TouchableOpacity } from 'react-native';

export default function App() {
  const [screen, setScreen] = useState('main'); // main, hospital, refuseReason, emergency
  const [refuseReason, setRefuseReason] = useState('');
  const [symptomLevel, setSymptomLevel] = useState('');

  if (screen === 'main') {
    return (
      <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
        <Button title="병원 전용" onPress={() => setScreen('hospital')} />
        <Button title="119 전용" onPress={() => setScreen('emergency')} />
      </View>
    );
  }

  if (screen === 'hospital') {
    return (
      <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
        <Button title="확인" onPress={() => alert('확인되었습니다')} />
        <Button title="거절" onPress={() => setScreen('refuseReason')} />
      </View>
    );
  }

  if (screen === 'refuseReason') {
    return (
      <View style={{ flex: 1, padding: 20 }}>
        <Text>거절 사유를 입력하세요:</Text>
        <TextInput
          style={{ borderWidth: 1, padding: 10, marginVertical: 10 }}
          multiline
          numberOfLines={4}
          value={refuseReason}
          onChangeText={setRefuseReason}
          placeholder="사유 입력"
        />
        <Button title="제출" onPress={() => alert(`사유: ${refuseReason}`)} />
        <Button title="뒤로" onPress={() => setScreen('hospital')} />
      </View>
    );
  }

  if (screen === 'emergency') {
    return (
      <View style={{ flex: 1, padding: 20 }}>
        <Button title="CALL" onPress={() => alert('119에 전화 연결 중')} />
        <Text style={{ marginVertical: 10 }}>증상 정도를 선택하세요:</Text>
        <TouchableOpacity onPress={() => setSymptomLevel('경증')}>
          <Text style={{ padding: 10, backgroundColor: symptomLevel === '경증' ? 'lightblue' : 'white' }}>경증</Text>
        </TouchableOpacity>
        <TouchableOpacity onPress={() => setSymptomLevel('중증')}>
          <Text style={{ padding: 10, backgroundColor: symptomLevel === '중증' ? 'lightblue' : 'white' }}>중증</Text>
        </TouchableOpacity>
        <TouchableOpacity onPress={() => setSymptomLevel('위급')}>
          <Text style={{ padding: 10, backgroundColor: symptomLevel === '위급' ? 'lightblue' : 'white' }}>위급</Text>
        </TouchableOpacity>
        <Text>선택된 증상 정도: {symptomLevel}</Text>
        <Button title="뒤로" onPress={() => setScreen('main')} />
      </View>
    );
  }

  return null;
}

