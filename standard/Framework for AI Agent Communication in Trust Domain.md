# Title: Framework for AI Agent Communication in Trust Domain

filename : draft-<ietf-wgname-docname>-00.txt

## Status of this Memo

This Internet-Draft is submitted in full conformance with the provisions of BCP 78 and BCP 79. 
This Internet-Draft is submitted in full conformance with the provisions of BCP 78 and BCP 79. This document may not be modified, and derivative works of it may not be created, and it may not be published except as an Internet-Draft.
This Internet-Draft is submitted in full conformance with the provisions of BCP 78 and BCP 79. This document may not be modified, and derivative works of it may not be created, except to publish it as an RFC and to translate it into languages other than English.
This document may contain material from IETF Documents or IETF Contributions published or made publicly available before November 10, 2008. The person(s) controlling the copyright in some of this material may not have granted the IETF Trust the right to allow modifications of such material outside the IETF Standards Process.  Without obtaining an adequate license from the person(s) controlling the copyright in such materials, this document may not be modified outside the IETF Standards Process, and derivative works of it may not be created outside the IETF Standards Process, except to format it for publication as an RFC or to translate it into languages other than English.
Internet-Drafts are working documents of the Internet Engineering Task Force (IETF), its areas, and its working groups.  Note that other groups may also distribute working documents as Internet-Drafts.
Internet-Drafts are draft documents valid for a maximum of six months and may be updated, replaced, or obsoleted by other documents at any time.  It is inappropriate to use Internet-Drafts as reference material or to cite them other than as "work in progress."
The list of current Internet-Drafts can be accessed at http://www.ietf.org/ietf/1id-abstracts.txt
The list of Internet-Draft Shadow Directories can be accessed at http://www.ietf.org/shadow.html
This Internet-Draft will expire on April 16, 2009.

## Copyright Notice

Copyright (c) 2025 IETF Trust and the persons identified as the document authors. All rights reserved.
This document is subject to BCP 78 and the IETF Trust’s Legal Provisions Relating to IETF Documents (http://trustee.ietf.org/license-info) in effect on the date of publication of this document. Please review these documents carefully, as they describe your rights and restrictions with respect to this document. Code Components extracted from this document must include Simplified BSD License text as described in Section 4.e of the Trust Legal Provisions and are provided without warranty as described in the Simplified BSD License.
This document is subject to BCP 78 and the IETF Trust’s Legal Provisions Relating to IETF Documents (http://trustee.ietf.org/license-info) in effect on the date of publication of this document. Please review these documents carefully, as they describe your rights and restrictions with respect to this document. 

## Abstract

<Type your abstract here. Typically 5-10 lines, never less than 3 lines nor more than 20 lines> 

## Table of Contents

1. Overview	3
1.1. Document Structure	3
1.2. Terms and Definitions	3
2. Overview of the operation	3
2.1. Roles	3
2.2. Protocol Flow	4
3. Digital ID	5
4. Tasks	6
4.1. Task Definition	6
4.2. Task Status	6
5. Communication mode	6
6. Multimodality	6
7. Capability Registration	7
8. Capability Discovery	7
9. Session management	7
10. Routing	7
11. Protocol Properties	7
11.1. Application layer	7
11.2. Transmission layer	7
12. Formal Syntax	7
13. Security Considerations	7
14. IANA Considerations	7
15. Conclusions	7
16. References	8
16.1. Normative References	8
16.2. Informative References	8
17. Acknowledgments	8
Appendix A. <First Appendix>	9
A.1. <First Header level>	9
A.2. <Second Header level 1>	9
A.2.1. <H2>	10
A.2.1.1. <H3>	10
A.2.1.1.1. <H4>	10
A.2.1.1.1.1. <H5>	10


## 1. Overview  ——华为、移动

With the development of AI agent technology, its application scenarios have been continuously expanding. From initial simple task execution to complex collaborative tasks among multiple agents, agents have demonstrated great potential in various fields. This multi-agent collaboration model can fully leverage the strengths of individual agents, improving the quality and efficiency of task execution. However, as the demand for multi-agent collaboration grows, defining standardized communication protocols among agents to achieve wide-area interconnection, cross-domain interoperability, and secure collaboration has become an urgent issue to address.
To meet the communication needs of AI agents and promote the widespread services of multi-agent collaboration, it is imperative to define standardized agent communication protocols that support interconnection, interoperability, and secure scalability between agents in trust domain.
### 1.1. Objectives
- Standardization: Establish a unified communication protocol standard to enable seamless communication and interoperability among agents.
- Wide-area interconnection: Support stable and efficient connections for agents across wide areas, ensuring that information exchange between agents is not restricted by geographical boundaries, and meeting the communication needs of agents in various scenarios.
- Security and scalability: Build a comprehensive security mechanism to ensure data security, privacy protection, and identity authentication during agent communication, preventing attacks and data leakage. In addition, the protocol should have good scalability to adapt to the continuous development of agent technologies and emerging new requirements, facilitating functional upgrades and optimizations of the protocol.
### 1.2. Scope
From the perspective of network service domain division, future agents can be simply categorized into 3 types based on their deployment locations: terminal-side agents, network-side agents, and agents outside the network. This draft mainly focuses on the communication between agents directly managed within the operator's network, i.e. the communication between the first two types of agents:
1. Communication between different terminal-side agents registered in the same network service domain.
2. Communication between terminal-side agents and network-side agents registered in the same network service domain.
3. Communication between network-side agents registered in the same network service domain.
Furthermore, the communication between agents registered in different network domains is not within the scope of this discussion.
### 1.3. Terms and Definitions
- Task: Task is actions required to achieve a specific goal. These actions can be physical or cognitive.
- Task chain: A Task chain defines an ordered set of tasks and ordering constraints that is to be applied to, e.g., packets, frames, or flows. The implied order may not be a linear progression as the architecture allows for task chain of more than one branch, and also allows for cases where there is flexibility in the order in which tasks need to be applied.
- Coordinator Agent: An agent that receives tasks and decomposes or distributes tasks to other agents.
- Execution Agent:	An agent responsible for executing tasks distributed by the Coordinator Agent.

## 2. Overview of the operation
### 2.1. Roles
The Agent communication protocol defines three roles:
- AI Agent
An automated intelligent entity that achieves a specific goal (autonomously or not) on behalf of another entity, by e.g. interacting with its environment, acquiring contextual information, reasoning, self-learning, decision-making, and executing tasks (independently or in collaboration with other AI Agents).
- Agent Registration Server
The server enables Agents to register their capabilities, and discover each other’s capabilities based on intent，task or other information.
- Agent Communication Server
The server enables Agents to communicate and collaborate with each other, which provides session management and routing function.
### 2.2. Protocol Flow  

![Protocol Flow](./pic/pic.jpg)

Figure 1: Abstract Protocol Flow   

The abstract flow illustrated in Figure 1 describes the interaction between the three roles and includes the following steps:
(A)  The AI Agent B requests to register its capabilities and related attributes to Agent Registration Server.
(B)  The Agent Registration Server authenticates the AI Agent B’s capabilities and then stores them, e.g., in its local database.
(C)  AI Agent A initiates a capability discover request to the Agent Registration Server, the request includes the intent, task or other information.
(D)  The Agent Registration Server matches the intent or task with the capabilities stored in its local database, and responses with matched AI Agents list to the AI Agent A.
Option1:
(E)  The AI Agent A selects AI Agent B from the list and sends a communication request to AI Agent B via Agent Communication Server.
(F)  The Agent Communication Server establishes the session and routes the message to AI Agent B.
(G)  The AI Agent B receives the communication request and sends a response to the Agent Communication Server.
(H)  The Agent Communication Server transfers the response to the AI Agent A.
Option2:
(E’) The AI Agent A selects AI Agent B from the list and sends a communication request to AI Agent B directly.
(F’) The AI Agent B receives the communication request and sends a response to the AI Agent A.

## 3. Digital ID
The digital identity mechanism is used for the registration, discovery and communication flows.
- Registration: digital identity contains a global unique identifier of AI agent as a basis for authentication and addressing during communication flow. Several agent-related attributes (capabilities/skills/services) are contained in the digital identity and registered with the identifier at the same time. The related credentials in the digital identity can be used for the verification.
- Discovery: the registered AI agent can then be discovered by other agents based on either identifier or capabilities. The agent can be discovered across different domains.
- Communication: one AI agent can communicate with the other AI agent, by sending an initial message with the identifier obtained from the discovered digital identity. The network can use this identifier for addressing and routing the message to the target AI agent. 
- Authentication: during the communication establishment, both AI agents can use the credentials for the identifier for authentication. Attributes can be negotiated after the authentication.
- Authorization: compared to human communication, AI agent communication needs to be explicitly authorized at all time. The attribute-based authorization mechanism can support both direct agent-agent authorization and delegated authorization, even for the user authorization.
In order to fulfill the requirements mentioned above, we suggest to introduce the W3C Decentralized Identifier (DID) and Verifiable Credential (VC) standards as the basic digital identity components.
- DID: The core DID specification does not require implementers to use specific computational infrastructure to build decentralized identifiers, allowing us to fully leverage existing mature technologies and well-established network infrastructure to build DIDs.
- VC: The VC can be used as container of attributes of an AI agent. The attributes of an AI agent may come from different sources which can be verified by the VC. This will help increase the interoperability of cross-domain communications.

## 4. Agent Description——ANP撰写
Agent Description (AD) exists in document form. The AD document serves as the entry point to access an agent, functioning similarly to a website homepage. Other agents can obtain information such as the agent's name, affiliated entity, functionalities, products, services, and interaction APIs or protocols from this AD document. With this information, data communication and collaboration between agents can be achieved.
### 4.1. Agent Description Document Format
The Agent Description (AD) document serves as the external entry point for an agent and can be provided in either of the following formats:
#### 4.1.1. Natural Language Format
Leveraging advancements in AI capabilities, the AD document can be entirely described using natural language.
#### 4.1.2. Structured Format（recommended）
Since different agents may utilize varying models with distinct capabilities, a structured approach is recommended for ensuring consistent and accurate interpretation of the same data across diverse models.
Structured Format supports multiple document types:
- JSON (Recommended)
- JSON-RPC
- Other structured document formats
### 4.2. Agent Information Interaction Mechanism
The system employs an information interaction mechanism analogous to "web crawlers." Specifically, agents utilize URLs to interconnect externally provided resources (e.g., information, interfaces) through agent description documents, forming a networked ecosystem. Other agents can then operate like crawlers, selectively retrieving appropriate resources to local systems based on the described metadata, where subsequent decision-making and processing occur autonomously.
Advantages of the Web-Crawler-like Information Interaction Mode：
- Compatibility with Existing Internet Architecture: Facilitates search engine indexing of agent-publicized information, enabling the creation of an efficient agent data network.
- Enhanced Privacy Protection: Pulling remote data to local systems for contextual processing mitigates user privacy leakage risks inherent in task-delegation models.
- Inherent Hierarchical Structure: Supports scalable interactions among a large number of agents.
Agent description documents include the following two types of resources:
#### 4.2.1. Informatica
Agents may provide the following types of data：
- Textual files (e.g.： .txt, .csv, .json)
- Image files (e.g.： .jpg, .png, .svg)
- Video files (e.g.： .mp4, .mov, .webm)
- Audio files (e.g.： .mp3, .wav, .aac)
- Other files
#### 4.2.2. Interface
Agent interfaces are categorized into two types:
- Natural Language Interface
-- Enables agents to deliver personalized services through natural language interaction.
-- Supports human-like communication and adaptive responses.
- Structured Interface
-- Facilitates efficient and standardized service delivery via predefined protocols.
-- Ensures interoperability and machine-to-machine automation.
### 4.3. Security Mechanism
Security configuration in Agent Description (AD) documents is mandatory. The security definition must be activated through the security member at the agent level. This configuration constitutes the required security mechanism for agent interactions.
- Global Scope: When security is declared at the root level of an AD document, all resources within the document must enforce this security mechanism for access.
- Resource-Specific Scope: If security is defined within an individual resource, access to that resource is granted only when the specified security conditions are met.
- Precedence Rule: In cases where resource-level security conflicts with root-level security, the resource-level definition takes precedence.
### 4.4. Integrity Verification
To prevent malicious tampering, impersonation, or reuse of Agent Description (AD) documents, a verification mechanism Proof is incorporated into the AD document structure. 
The definition of Proof shall comply with the specification: [https://www.w3.org/TR/vc-data-integrity/#defn-domain].

## 5. Tasks——华为云核，ANP参与
### 5.1. Task Definition
任务定义，任务作用, 任务拆分，父子任务
### 5.2. Task Status
任务状态和切换、状态通知

## 6. Communication mode----华为数通
通信模式(P2P，群组)

## 7. Multimodality----华为2012
支持多模态交互：文本、图片、文件等，支持多模态数据分流或者高效流复用

## 8. Capability Registration——电信撰写，移动参与
能力注册流程和关键消息、参数
The registration procedure for an AI Agent in trust domain can refer to steps (A)-(B) in Figure 1. In trust domain scenario, the AI Agents need to register their attributes to a centralized Agent Registration Server, which can be an Agent, a network function, a third-party server, etc. For example, in 6G core network, the Agent Registration Server can evolve and enhance based on the Network Repository Function (NRF), supporting the registration of the traditional network functions and the network Agents. 
The parameters that an Agent needs to register in a trust domain (step A) may include:
- Name: The name of the Agent, which may not be unique and typically represented as a string.
- ID: The global unique ID of the Agent configured by the network operator.
- Description: Unlike the AD in section 4, the description in the Agent Register information should provide a more concise summary of the Agent’s relevant details based on natural language, typically serving as an abstract of the AD.
- Address: The access address of the Agent, which might be an URL, FQDN, ICN address, etc.
- Version: The current version of the Agent, which can be updated in real-time.
- Capabilities: The capabilities supported by the Agent, including the communication capabilities, interaction modes and multimodal capabilities, etc. The communication capabilities refer to the communication protocols supported by the Agent, such as http/2, http/3, A2A, ANP, MCP, etc. The interaction modes may include request-response and subscription-notification and others. The multimodal capabilities refer to the data modalities that the agent can process, such as text, images, video, etc.
- Services: The services that the agent can provide. For example, in 6G core network the services may include communication service, AI service, sensing service, computing service, data service, etc. A network Agent may support one or more of these network services.
- Skills: A list of detailed description of the skills supported by the Agent. The content of each skill include the name, ID, corresponding services, brief abstract, required input, etc. For example, an Agent deployed in 6G core network support skills named “Policy Control” and “User Location Prediction”. Among these, “Policy Control” corresponds to communication service and requires inputs including user policy-related information; “User Location Prediction” corresponds to AI service and requires inputs including user identification and historical location information.
- Interfaces: The network interfaces that the agent can provide.
- Security related information: For example, the licenses, authentication credentials, keys of the Agent.
Then the Agent Registration Server locally sores the registration information of the Agent. Upon successful registration, the Agent Registration Server returns a registration response to the Agent (step B).


## 9. Capability Discovery——移动

In the previous chapter, the registration mechanism of AI agents was introduced, which relies on the Agent Registration Server to complete the registration of AI agents in the trusted domain, including their own capabilities, identity information, and other details. The discovery of AI agents also depends on the Agent Registration Server, and the discovery process consists of two phases: "query matching" and "result feedback".

** Query Matching
The initiating AI Agent A send queries to the registration server, and the server screens and matches the target agents based on the capability database.The query request can be sent via the MQTT Publish protocol, and the request parameters should be structured (to avoid ambiguous descriptions). Examples are as follows:

    Requirement type: "Medical image analysis"
    Location range: "Within 1 kilometer of base station BS-001"
    Real-time requirement: "Latency ≤ 100ms"
    Security level: "Medical qualification VC is required"

The registration server conducts screening according to the following priority order:
    First priority: Identity validity (whether there is a valid VC)
    Second priority: Location and real-time performance (whether it is within the specified area and meets the latency requirement)
    Third priority: Resource redundancy (e.g., agents with a computing power idle rate ≥ 50% are given priority)

After the matching is completed, a "target agent list" is generated, which includes the DID, communication address, and capability matching degree of each agent.

** Result Feedback
The registration server feeds back the matched results to the initiator AI agent A, and the initiator starts the session establishment based on the results. During this process, the registration server pushes the "target agent list". After receiving the list, the initiator gives priority to select the target agent with the highest matching priority, and makes choices based on the "communication address" and "protocol preference" in the list. For instance, if the target agent has preferences for real-time interaction or non-real-time data synchronization, the sender can select appropriate communication protocols as needed.


## 10. Session  management——移动
建立会话、会话状态、上下文管理
After discovering the peer Agent (e.g., Agent D), the local Agent (e.g., Agent S) needs to establish a session with it to communicate. After the task is completed. the relevant session resources can be released.
### 10.1 Session Establishment and Control
Before communicating with Agent D, Agent S should first establish a secure connection with the Agent Communication Server. Prior to this, Agent S must undergo authentication by the Agent Communication Server. Similarly, Agent D also needs to be authenticated by the Agent Communication Server to establish a secure connection.
Therefore, the Agent Communication Server needs to support the status maintenance of the attached Agents, such as the status of Agent S and Agent D. In other words, there should be an Agent status table on the Agent Communication Server, and the table should include information about Agent ID, Agent IP, etc.
In order to communicate with Agent D, Agent S initiates a session establishment request to the Agent Communication Server. After verifying its permissions, the Agent Communication Server proceeds to establish the session, for example, by assigning a globally unique Session ID to the new session. This ID will be used throughout the entire session lifecycle to correlate all activities and data. Correspondingly, the Agent Communication Server needs to maintain a session table, which includes information about all Agents involved in the session, especially information about the session initiator.
### 10.2 Differentiated QoS Guarantees
During the session establishment, Agent S can provide the relevant QoS requirements for the session. Consequently, the Agent Communication Server can prioritize the processing and forwarding of messages according to these requirements to ensure the session's QoS.
## 11. Routing  ----数通
会话路由机制 

## 12. Protocol Properties
### 12.1. Application layer----华为云核
应用层协议栈
### 12.2. Transmission layer——联通
传输层协议栈（支持QoS差异化、支持多模数据分流或者流复用，移动性保证）
Transport layer protocols such as QUIC, TCP, and UDP should be designed or enhanced to support agent session management and routing mechanisms.

QoS Guarantee: A multi-level QoS system should be established based on the differences in data types and service requirements within agent sessions. The transport layer should convert QoS priorities assigned to agent services into transport layer scheduling priorities while implementing resource isolation. Additionally, in mobile scenarios, it should dynamically optimize and update QoS parameters according to revised QoS rules.

Multimodal Data Offloading/Data Stream Multiplexing: Multi-path transmission capabilities (i.e., MPTCP, MPQUIC) should be adopted to support flexible transmission management of multi-source data from agents. Multimodal data can be allocated to appropriate transmission paths based on data types and network link conditions to prevent congestion on a single link. Meanwhile, data stream multiplexing can be employed, where data from multiple sessions is encapsulated into transmission units. Data identifiers are introduced to distinguish data ownership, and isolation mechanisms ensure no mutual interference occurs during data stream multiplexing.

Mobility Management: It should support service continuity and session persistence for agent users in mobile scenarios. For instance, QUIC's Connection ID can be leveraged to support mobility. During an agent's movement, multi-path transmission and fast handover should be supported. Upon receiving a handover notification, the transport layer should either transmit unfinished data packets to the new link or switch data to a backup link, thereby enabling mobility management for agent communication.

## 13. Formal Syntax
The following syntax specification uses the augmented Backus-Naur Form (BNF) as described in RFC-2234 [RFC2234].
<Define your formal syntax here.>

## 14. Security Considerations----华为云核
留口子，但是不展开

## 15. IANA Considerations
<Add any IANA considerations>

## 16. Conclusions-----华为云核
描述体现存在多个trust domain，涉及数字身份转换、能力注册发现、路由等，未来需要研究

## 17. References
### 17.1. Normative References
[1]	Bradner, S., "Key words for use in RFCs to Indicate Requirement Levels", BCP 14, RFC 2119, March 1997.
[2]	Crocker, D. and Overell, P.(Editors), "Augmented BNF for Syntax Specifications: ABNF", RFC 2234, Internet Mail Consortium and Demon Internet Ltd., November 1997.
[RFC2119]	Bradner, S., "Key words for use in RFCs to Indicate Requirement Levels", BCP 14, RFC 2119, March 1997.
[RFC2234]	Crocker, D. and Overell, P.(Editors), "Augmented BNF for Syntax Specifications: ABNF", RFC 2234, Internet Mail Consortium and Demon Internet Ltd., November 1997.
17.2. Informative References
[3]	Faber, T., Touch, J. and W. Yue, "The TIME-WAIT state in TCP and Its Effect on Busy Servers", Proc. Infocom 1999 pp. 1573-1583.
[Fab1999]	Faber, T., Touch, J. and W. Yue, "The TIME-WAIT state in TCP and Its Effect on Busy Servers", Proc. Infocom 1999 pp. 1573-1583.

## 18. Acknowledgments
<Add any acknowledgements>
This document was prepared using 2-Word-v2.0.template.dot.

## Appendix A. <First Appendix>

### A.1. <First Header level>

<Text>
	
### A.2. <Second Header level 1>
	
Copyright (c) 2025 IETF Trust and the persons identified as authors of the code. All rights reserved.
Redistribution and use in source and binary forms, with or without modification, is permitted pursuant to, and subject to the license terms contained in, the Simplified BSD License set forth in Section 4.c of the IETF Trust’s Legal Provisions Relating to IETF Documents (http://trustee.ietf.org/license-info).
Copyright (c) 2025 IETF Trust and the persons identified as authors of the code. All rights reserved.
Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:
- Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer. 
- Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution. 
- Neither the name of Internet Society, IETF or IETF Trust, nor the names of specific contributors, may be used to endorse or promote products derived from this software without specific prior written permission.
THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

#### A.2.1.

<Text>
	
##### A.2.1.1.

<Text>
	
###### A.2.1.1.1.

<Text>
	
Authors’ Addresses
<Firstname> <Lastname>
<Affiliation>
<Address>
	
Phone: <optional>
Email: <Your email address>

<Firstname> <Lastname>
<Affiliation>
<Address>
	
Phone: <optional>
Email: <Your email address>

