```css
.header {
  background-color: #1890ff; /* Updated header color */
  padding: 20px;
  text-align: center;
}

.header-content {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}

.ant-table {
  background: #fff;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  margin-top: 20px;
  font-size: 14px;
  width: 100%; /* Set table width to 100% */
}

.ant-table th {
  background-color: #1890ff; /* Updated header color */
  color: white;
  font-size: 16px; /* Adjusted font size for headers */
  font-weight: bold;
  padding: 12px; /* Increased padding for headers */
  border: none; /* Remove header borders */
}

.ant-table td {
  padding: 12px; /* Increased padding for table cells */
  font-size: 14px;
  background-color: #f6f6f6; /* Light gray background for table cells */
  border-bottom: 1px solid #ddd; /* Border color for table rows */
  height: 50px; /* Fixed height for table cells */
}

.ant-table tr:hover {
  background-color: #e6f7ff; /* Light blue on hover */
}

.gold-row {
  background-color: #fffde7; /* Light yellow for gold performers */
}

.silver-row {
  background-color: #f3f6f9; /* Light gray for silver performers */
}

.bronze-row {
  background-color: #f9f9f9; /* Slightly darker gray for bronze performers */
}

.ant-table-cell {
  display: flex;
  align-items: center; /* Center align content vertically */
}

.ant-table-cell-with-badge {
  justify-content: center; /* Center align badge horizontally */
}

.top-performer-card {
  background-color: #fff;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  padding: 20px;
  text-align: center;
  margin: 10px;
  width: 220px;
  transition: transform 0.2s;
}

.top-performer-card:hover {
  transform: scale(1.05);
}

.badge-container {
  display: flex;
  align-items: center;
  justify-content: center;
}

.performance-score {
  display: block;
  margin: 10px 0;
}

.sparkles {
  position: relative;
  width: 100%;
  height: 50px; /* Adjust height as needed */
  overflow: hidden;
}

.sparkle {
  position: absolute;
  width: 10px;
  height: 10px;
  border-radius: 50%;
  animation: sparkle 1.5s infinite;
}

@keyframes sparkle {
  0% {
    opacity: 0;
    transform: scale(0.5);
  }
  50% {
    opacity: 1;
    transform: scale(1.2);
  }
  100% {
    opacity: 0;
    transform: scale(1);
  }
}

.sparkle:nth-child(1) {
  background-color: #ff0000;
  left: 10%;
  top: 10%;
  animation-delay: 0s;
}

.sparkle:nth-child(2) {
  background-color: #00ff00;
  left: 30%;
  top: 20%;
  animation-delay: 0.3s;
}

.sparkle:nth-child(3) {
  background-color: #0000ff;
  left: 50%;
  top: 10%;
  animation-delay: 0.6s;
}

.sparkle:nth-child(4) {
  background-color: #ffff00;
  left: 70%;
  top: 20%;
  animation-delay: 0.9s;
}

.sparkle:nth-child(5) {
  background-color: #ff00ff;
  left: 90%;
  top: 10%;
  animation-delay: 1.2s;
}

```
```javascript
import React from "react";
import { Badge, Typography, Button } from "antd";
import img1 from "./img/gold.png";
import img2 from "./img/silver.png";
import img3 from "./img/bronze.png";
import "./GamificationUI.css";

const { Text } = Typography;

const TopPerformerCard = ({ agent, showSparkles, onCelebrate }) => {
  const getBadgeImage = (score) => {
    if (score > 400) return img1; // Gold badge
    if (score > 300) return img2; // Silver badge
    return img3; // Bronze badge
  };

  return (
    <div className="top-performer-card">
      <div className="badge-container">
        <img
          src={getBadgeImage(agent.performance_score)}
          alt="Badge"
          style={{ width: "50px", height: "50px" }}
        />
        <Text strong style={{ marginLeft: "10px" }}>
          {agent.agent_name.charAt(0).toUpperCase() + agent.agent_name.slice(1)}
        </Text>
      </div>
      <Text className="performance-score">
        Performance Score: {agent.performance_score}
      </Text>
      <Badge
        count={
          agent.performance_score > 400
            ? "Gold"
            : agent.performance_score > 300
            ? "Silver"
            : "Bronze"
        }
        style={{
          backgroundColor:
            agent.performance_score > 400
              ? "#FFD700"
              : agent.performance_score > 300
              ? "#C0C0C0"
              : "#cd7f32",
        }}
      />
      {showSparkles && (
        <div className="sparkles">
          <div className="sparkle"></div>
          <div className="sparkle"></div>
          <div className="sparkle"></div>
          <div className="sparkle"></div>
          <div className="sparkle"></div>
        </div>
      )}
      <Button
        type="primary"
        onClick={onCelebrate} // Call onCelebrate when clicked
        style={{ marginTop: "10px", backgroundColor: "green" }}
      >
        Celebrate Top Performer
      </Button>
    </div>
  );
};

export default TopPerformerCard;

```
```javascript
import React, { useEffect, useState } from "react";
import { Table, Layout, Typography, Divider, Button, Modal } from "antd";
import axios from "axios";
import TopPerformerCard from "./TopPerformerCard";
import CarProgress from "./CarProgress";
import "./GamificationUI.css";
import img1 from "./img/gold.png";
import img2 from "./img/silver.png";
import img3 from "./img/bronze.png";

const { Header, Content } = Layout;
const { Title, Text } = Typography;

const GamificationUI = () => {
  const [agents, setAgents] = useState([]);
  const [topPerformer, setTopPerformer] = useState(null);
  const [points, setPoints] = useState(0);
  const [isGameVisible, setIsGameVisible] = useState(false);
  const [userMetrics, setUserMetrics] = useState(null);
  const [expandedRowKeys, setExpandedRowKeys] = useState([]);
  const [celebrateSparkles, setCelebrateSparkles] = useState(false);
  const targetTalkTime = 9000;
  const targetCallsCount = 3;
  const targetCustomerSentiments = 30;
  const targetNonTalkTime = 10000;

  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await axios.get(
          "https://rrjboaljfmf5vyhuienk5mzszi0weebt.lambda-url.us-east-1.on.aws/"
        );
        setAgents(response.data);
        const topAgent = response.data.reduce(
          (max, agent) =>
            agent.performance_score > max.performance_score ? agent : max,
          response.data[0]
        );
        setTopPerformer(topAgent);
      } catch (error) {
        console.error("Error fetching data:", error);
      }
    };
    fetchData();
  }, []);

  const handleChallengeComplete = () => {
    setIsGameVisible(true);
    const userAgent = agents.find(
      (agent) => agent.agent_id === "872d83df-69ec-47ba-9458-5bfb3fa9970f"
    );
    setUserMetrics(userAgent);
  };

  const handleCelebrate = () => {
    setCelebrateSparkles(true);
    setTimeout(() => {
      setCelebrateSparkles(false);
    }, 3000);
  };

  const handleSubmit = () => {
    let score = 0;
    let feedback = "";
    if (userMetrics.agent_talk_time < targetTalkTime) {
      feedback +=
        "Increase your agent talk time to improve your performance.\n";
    } else {
      score += 25;
    }
    if (userMetrics.agent_calls_count < targetCallsCount) {
      feedback +=
        "Increase your agent calls count to improve your performance.\n";
    } else {
      score += 25;
    }
    if (userMetrics.customer_sentiments_score < targetCustomerSentiments) {
      feedback +=
        "Increase your customer sentiments score to improve your performance.\n";
    } else {
      score += 25;
    }
    if (userMetrics.agent_non_talk_time > targetNonTalkTime) {
      feedback +=
        "Decrease your agent non-talk time to improve your performance.\n";
    } else {
      score += 25;
    }
    setPoints(points + score);
    alert(
      `Congratulations! You earned ${score} points.\n\nFeedback:\n${feedback}`
    );
    setIsGameVisible(false);
  };

  const columns = [
    {
      title: "Agent Name",
      dataIndex: "agent_name",
      key: "agent_name",
      render: (text, record) => (
        <Text
          style={{
            fontSize: "16px",
            fontWeight: "bold",
            textTransform: "capitalize",
          }}
        >
          {text.charAt(0).toUpperCase() + text.slice(1)}
        </Text>
      ),
      width: "25%",
    },
    {
      title: "Performance Score",
      dataIndex: "performance_score",
      key: "performance_score",
      render: (text) => <Text style={{ fontSize: "16px" }}>{text}</Text>,
      width: "20%",
    },
    {
      title: "Progress",
      dataIndex: "performance_score",
      key: "progress",
      render: (score) => <CarProgress score={score} />,
      width: "30%",
    },
    {
      title: "Badge",
      dataIndex: "performance_score",
      key: "badge",
      render: (score) => (
        <div
          style={{
            display: "flex",
            justifyContent: "center",
          }}
        >
          <img
            src={score > 400 ? img1 : score > 300 ? img2 : img3}
            alt="Badge"
            style={{ width: "50px", height: "50px" }}
          />
        </div>
      ),
      width: "25%",
    },
  ];

  const topPerformers = agents.filter((agent) => agent.performance_score > 400);
  const expandedRowRender = (record) => {
    return (
      <div>
        <Text>Agent Sentiments Score: {record.agent_sentiments_score}</Text>
        <br />
        <Text>
          Customer Sentiments Score: {record.customer_sentiments_score}
        </Text>
        <br />
        <Text>Agent Talk Time: {record.agent_talk_time}</Text>
        <br />
        <Text>Agent Non-Talk Time: {record.agent_non_talk_time}</Text>
        <br />
        <Text>Agent Calls Count: {record.agent_calls_count}</Text>
      </div>
    );
  };

  return (
    <Layout style={{ minHeight: "100vh" }}>
      <Header className="header">
        <div className="header-content">
          <Title style={{ color: "white" }} level={2}>
            Agent Performance Leaderboard
          </Title>
        </div>
      </Header>
      <Content style={{ padding: "20px" }}>
        {topPerformer && (
          <div className="top-performer-container">
            <TopPerformerCard
              key={topPerformer.agent_id}
              agent={topPerformer}
              showSparkles={celebrateSparkles}
              onCelebrate={handleCelebrate}
            />
          </div>
        )}
        {topPerformers.length > 0 && (
          <div className="top-performers">
            <Divider orientation="left">Top Performers</Divider>
            <Text>
              Congratulations to our top performers who have achieved the
              coveted Gold Badge! Keep up the excellent work and aim for the
              stars!
            </Text>
            <div className="top-performers-list">
              {topPerformers.map((agent) => (
                <TopPerformerCard
                  key={agent.agent_id}
                  agent={agent}
                  showSparkles={celebrateSparkles}
                  onCelebrate={handleCelebrate}
                />
              ))}
            </div>
          </div>
        )}
        <Button type="primary" onClick={handleChallengeComplete}>
          Complete Challenge
        </Button>
        <Text style={{ marginLeft: "10px" }}>Points: {points}</Text>
        <Table
          className="agent-performance-table"
          dataSource={agents}
          columns={columns}
          rowKey="agent_id"
          pagination={false}
          expandedRowKeys={expandedRowKeys}
          expandedRowRender={expandedRowRender}
          onExpand={(expanded, record) => {
            const newExpandedRowKeys = expanded
              ? [...expandedRowKeys, record.agent_id]
              : expandedRowKeys.filter((key) => key !== record.agent_id);
            setExpandedRowKeys(newExpandedRowKeys);
          }}
          rowClassName={(record) => {
            if (record.performance_score > 400) {
              return "gold-row";
            } else if (record.performance_score > 300) {
              return "silver-row";
            } else {
              return "bronze-row";
            }
          }}
          size="small"
          bordered
        />
        <Modal
          title="Become the Top Performer!"
          visible={isGameVisible}
          onCancel={() => setIsGameVisible(false)}
          footer={null}
          width={600}
        >
          {userMetrics && (
            <div>
              <Text style={{ fontSize: "18px", fontWeight: "bold" }}>
                Current Metrics:
              </Text>
              <div style={{ marginTop: "10px" }}>
                <Text style={{ display: "block" }}>
                  Agent Talk Time: {userMetrics.agent_talk_time}
                </Text>
                <Text style={{ display: "block" }}>
                  Target: {targetTalkTime}
                </Text>
              </div>
              <div style={{ marginTop: "10px" }}>
                <Text style={{ display: "block" }}>
                  Agent Calls Count: {userMetrics.agent_calls_count}
                </Text>
                <Text style={{ display: "block" }}>
                  Target: {targetCallsCount}
                </Text>
              </div>
              <div style={{ marginTop: "10px" }}>
                <Text style={{ display: "block" }}>
                  Customer Sentiments Score:{" "}
                  {userMetrics.customer_sentiments_score}
                </Text>
                <Text style={{ display: "block" }}>
                  Target: {targetCustomerSentiments}
                </Text>
              </div>
              <div style={{ marginTop: "10px" }}>
                <Text style={{ display: "block" }}>
                  Agent Non-Talk Time: {userMetrics.agent_non_talk_time}
                </Text>
                <Text style={{ display: "block" }}>
                  Target: {targetNonTalkTime}
                </Text>
              </div>
              <Button
                type="primary"
                onClick={handleSubmit}
                style={{ marginTop: "20px" }}
              >
                Submit
              </Button>
            </div>
          )}
        </Modal>
      </Content>
    </Layout>
  );
};

export default GamificationUI;

```

